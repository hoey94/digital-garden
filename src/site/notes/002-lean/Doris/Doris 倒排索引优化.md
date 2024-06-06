---
{"dg-publish":true,"permalink":"/002-lean/Doris/Doris 倒排索引优化/","dgPassFrontmatter":true}
---



在 Doris 的官方介绍里，2.0之后引入了「倒排索引」功能，说到倒排索引呢，我们一般第一想到的应该是 Elasticsearch、Solr 这样具有代表性的搜索引擎型的数据
库。  Elasticsearch 的核心技术实现，就是用的倒排索引，而它的好用程度也早就在工业界得到了验证，是一款非常成功的，将倒排索引这个技术落地的开源软件。至于2.0之后，Doris 也引入了这个倒排索引功能，好不好用，那么今天这篇文章，咱一起来测试验证一番。  

（_PS：本文基于 Doris2.0.2 进行验证测试_）

## **0. 文档介绍**

再一次打开 Doris 的官方文档发现，它变了，之前我在文章中吐槽的关于文档编排的缺陷，好像大部分都得到了改善。  

左侧的文档结构布局变得更加清晰合理，相对应的描述内容，也尽量摒弃了之前那种跨章节的“这里一坨，那里一块”的散乱式摆放模式，看得出来，这次的文档改进用心了，必须点个赞。  

文档关于倒排索引部分的描述，很容易就能在左侧的目录中找到，

![图片](https://mmbiz.qpic.cn/mmbiz_png/G1NpMCNMwLoJ56RkFCIgH0TQDXEvy3qhBhcjCjsFs3srsAkkibu2RFUxg5jypia175y26l6lG6UiauelrEreh0A9w/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

从描述内容来看，涵盖了对倒排索引的名词解释、功能、语法，以及案例说明，对一个初次接触的人来说，可以说是很全了，这里不做过多的赘述。


## **1. 为啥要支持倒排索引**

可能有同学会好奇，一个好端端的数据库，为什么突然要支持这个倒排索引的功能，对于这个疑点，我个人认为官方文档的解释还不够令我满意，这里谈谈我的看法：

> _我们知道，普通索引的实现方式，就是选定某个需要索引的字段之后，将整个字段值的内容，作为一个整体进行排序。_
> 
> _在使用时，我们通过对这个字段值，**整个内容的完全相等匹配**，来找到对应的记录，从而实现快速查找的目的。_
> 
> _但是呢，这种普通的索引方式，**只适合那种字段值比较短的情况**，比如数值类型、短的字符串类型等等。_
> 
> _而如果我们遇到的场景是，需要存储的某个字段的值，包含的内容很长，比如是一篇文章，而我想在查找这些长字符串的内容时，给出的查询条件，只需要命中这些内容中的某个关键词，就能把相关的内容给匹配出来，那么针对这个查询需求，很显然，普通索引是没有办法胜任的(模糊匹配不能算哈)。_  
> 
> _于是这个时候，就得让倒排索引出马了。_

## **2. 怎么用**

从官方文档描述来看，创建倒排索引的方式有3种。  

**_第1种：在建表语句中直接指定；_**

**_第2种：通过 create index...on...using... 的方式进行后续添加；_**

**_第3种：通过 alter table... add index... using... 的方式进行后续添加。_**

我们知道，对于一个倒排索引来说，想要满足好的匹配查询体验，必须要有一个足够人性化的「分词器」，但是从目前 Doris 的官网来看，支持的还不够丰富：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/G1NpMCNMwLrnoXgTU8NkxTZalehiaDiada3NLyg5y3nm8PK0lUib64RFdIkKTHzWRylf4ITwr6qWuDdeicgyI0dwWQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

目前只有内置的4种分词方式，显然，对于这一点，是不及 ES 的，在我之前经历的项目中，为了满足个性化的分词要求，ES 是可以用插件的方式添加分词器，而且可以添加完全贴合业务搜索要求的分词字典，来达到精准分词的目的。  

今天这篇文章，咱暂时不跟 ES 做性能上的 PK，就单纯从 Doris 提供这个功能的实用性出发，看相比之前的普通索引方式，提供了哪些实用性的便利。  

## **3. 跑起来**

因为 Doris 的查询方式，用的都是标准的 SQL，所以对于创建了倒排索引字段的查询，同样也遵循普通 SQL 的查询方式，这一点，比 ES 要友好，毕竟 SQL 的普适性，要远高于 ES 的 DSL 语法。

从文档描述来看，其查询方式需要将原本的「=」号，更改为「MATCH_ANY」或者「MATCH_ALL」关键词。  

但是，你猜怎么着？

### **3.1 没有添加倒排索引情况下**

好奇心驱使，我**在一张压根就没有添加倒排索引的表里，用「MATCH_ANY」跟「MATCH_ALL」来查找关键词****，居然也可以**：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/G1NpMCNMwLrnoXgTU8NkxTZalehiaDiadaktvo11XmuZM0BxFD9Cuzdccxict9Yb6icyIk7ovNXbVJZaczkSw0dFdA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

_选取一张数据量近9百万的表_

![图片](https://mmbiz.qpic.cn/mmbiz_png/G1NpMCNMwLrnoXgTU8NkxTZalehiaDiada5WvwPRGLV5gnGNjubGfCIZHriaRvzpktRR3FTKJqcl9wzZdw8wPQpsA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

_建表语句(没有添加倒排索引)_

![图片](https://mmbiz.qpic.cn/mmbiz_png/G1NpMCNMwLrnoXgTU8NkxTZalehiaDiadaMnHZqw5Epeauvib7zhEwhLQJlY0wVXGoiayX8ibNII9m9UyEHdLOrZ7gA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

_利用MATCH_ANY、MATCH_ALL 对其查询_

而且查询结果符合预期，只不过呢，查询效率有些不尽如人意，在我这张总数据量近9百万的表中，查询时间为 **2.7秒** (查询多次，下同)。

不知道这么做(可以用全文检索的方式，对非倒排索引字段进行查询)是 Doris 官方的刻意为之，还是误打误撞导致的这个结果。

### **3.2 添加倒排索引情况下**

既然查询效率不尽如人意，那么接下来，我们对这两个条件字段分别添加倒排索引后，再来试试看。

**先给 domain 字段添加倒排索引：**

```sql
ALTER TABLE dns_logs ADD INDEX idx_domain(domain) USING INVERTED PROPERTIES("parser" = "english") COMMENT 'add inverted index for domain';
```

这个语句只会让该表的**新增数据**生效，那为了让存量数据也生效，需要执行下面这一步：  


![图片](https://mmbiz.qpic.cn/mmbiz_png/G1NpMCNMwLrnoXgTU8NkxTZalehiaDiada4KibH70Js3Utszhb65K0kB5YibqyqSAzl3A7eGmeMiaibYO7G9fAVGvTjw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

执行后，会触发后台对 domain 这个字段的历史数据处理，数据量越大，那么处理的时间就会越长。  

查看后台处理进度：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/G1NpMCNMwLrnoXgTU8NkxTZalehiaDiadaAu4FLwic8ksJiaibNQko1cOSIcP6O85sNmo5PunBAODSy8cGpNTicxWyzg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到，近9百万条数据，大概用了4秒钟就完成了 domain 这个字段的倒排索引创建过程。  

这个时候，我们来看一下，当查询条件中的一个字段完成倒排索引的创建之后，能带来多少的查询加速：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/G1NpMCNMwLrnoXgTU8NkxTZalehiaDiadaaNdqNQD0En9mLEh17Y0iaHq4MVv2q4anzqBjfmt6OtQz0w7UPrDPYLQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到，查询时间由原来的2.7秒，缩短为**0.46秒**，提速超过**2秒**。

**再****给 client_ip 字段添加倒排索引：**  

添加方式跟上面的 domain 字段一毛一样，具体过程这里就不赘述了。

最后查看创建进度：

![图片](https://mmbiz.qpic.cn/mmbiz_png/G1NpMCNMwLrnoXgTU8NkxTZalehiaDiadaT7q3mWv2AUBBctrblD3jtw9XhFBRrT9wLRGrytgyxLVs1cWY3fRibSw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到，通过对 client_ip 的历史数据创建倒排索引(近9百万条记录)，一共花了约2秒钟。

再次运行之前的查询语句，看两个字段都创建了倒排索引之后，其查询效率能提高多少：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/G1NpMCNMwLrnoXgTU8NkxTZalehiaDiadaSicm85XD9FrHDuQjaomutXAluoqmBniaWcgAouebhM5fI7zqV19fTrPA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到，这一次查询时间由之前的0.46秒，提升到**0.13秒**。
  

## **4. 使用感受**

通过以上的简单测试可以看出，Doris通过添加倒排索引之后，确实能有效提高全文检索的效率。  

这里有个我认为比较重要，但是官方文档没有提及的点，那就是，Doris 虽然对表中的字段添加了倒排索(带分词的)之后，**既可以对其字段进行关键词/字检索，同时，依然可以对其字段的全部内容进行等值检索**。

![图片](https://mmbiz.qpic.cn/mmbiz_png/G1NpMCNMwLrnoXgTU8NkxTZalehiaDiadaOoSoKZcyDoiaWunFIlN4JEvvZsBerS6GcMOJXGLr7dmy8GIz4A2cqHw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

_全文关键词检索方式_

![图片](https://mmbiz.qpic.cn/mmbiz_png/G1NpMCNMwLrnoXgTU8NkxTZalehiaDiadaVtvyIaB8N9M5HH1CEXE06H32M8iat1FDD09XichVFoP34m3VXwQT9XdA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

_全文等值检索方式_

可能对于这个问题，很多人会不以为然，但是如果你是 ES 的深度玩家，你就知道，ES 默认情况下是不支持这一点的，或者说，同一个字段，想要同时满足这两种检索方式，需要两种不同的分词策略。

因为对于 ES 来说，一旦你选择了一种分词策略，它就会把这个字段下的值，「全部切开后再保存」，而不会再单独保存一份这个字段的「整体值」，如果你需要保存这个字段的「整体值」，就得再添加一种新的分词策略(term分词)。

个人认为对于这一点来说，是要比 ES 更好用的。

另外，对于我比较关心的存储空间膨胀问题，这里可以看出来，

![图片](https://mmbiz.qpic.cn/mmbiz_png/G1NpMCNMwLrnoXgTU8NkxTZalehiaDiadaZVSwJljwJ0Ms09Od2LeupS626lpLo6g7CYunZdmR5L9p2DgVrTVdAg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)  

在添加了2个字段的倒排索引之后，空间膨胀了 **0.035GB**，个人觉得还行，毕竟，索引的本质不就是拿存储空间换查询效率嘛。  

最后，就是对于 Doris 的表，它的表结构、索引方式是可以随时变更的，这个就给我们的操作带来很大的柔性空间，算是它的优点。

而 ES 呢，虽然它预先定义的字段类型，跟索引方式在后期不可更改，但它的表字段个数却是柔性的，可以任意增加和减少，而且你可以为一个 ES 表添加一个灵活的「模板」来适配不同字段的类型，以及索引方式。

算各有优劣吧，不存在谁碾压谁一说。  


**最后**

这篇文章算是对 Doris 2.x 新增倒排索引功能的初步体验，总体来说还可以(毕竟从无到有嘛)，根据官方文档一路走下来，没有遇到坑，在提供了全文检索能力的同时，也确实能够提高查询效率(跟之前测试过几个闹眼子的提速手段相比，这次是真的)。

但是，你说就目前看到的功能，非得跟 ES 一较高下，我觉得多少有点幼稚和冲动，毕竟单纯从全文检索这个角度来看，现在的 Doris 肯定还嫩着呢。  

你觉得呢？

转自：[Doris的倒排索引功能，好使不？ (qq.com)](https://mp.weixin.qq.com/s/dJ65aGYNd7x-dTK4lbAPKA)