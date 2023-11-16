---
{"uid":20230711090245,"title":"Obsidian 插件：echarts 图表化展示你的笔记","tags":["obsidian","插件","图表生成"],"description":"Obsidian 插件：echarts 图表化展示你的笔记。一个可以在 obsidian 里运行 echarts 的插件，具体可以参考官方示例库代码。插件需要依赖 dataview 插件","author":"cuman","type":"basic","draft":false,"editable":false,"modified":20230712172437,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/obsidian-echarts/","dgPassFrontmatter":true}
---


# Obsidian 插件：echarts 图表化展示你的笔记

> [!Note] 插件名片
> - 插件名称：echarts
> - 插件作者：windily-cloud && Cuman
> - 插件说明：一个可以在 obsidian 里运行 echarts 的插件，具体可以参考官方示例库代码。插件需要依赖 dataview 插件
> - 插件分类：图表生成, 美化
> - 插件项目地址：[点我访问](https://github.com/cumany/obsidian-echarts)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?obsidian-echarts)

## 概述

obsidain-echarts 插件是一款自定义程度很高的插件，结合 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/dataview\|dataview]] 查询到的数据源，生成丰富的图表。echarts 插件是把 [Apache ECharts](https://echarts.apache.org/en/index.html) 库移植到了 obsidian 中，所以官方的示例代码稍加修改即可用于 obsidian 中。目前插件集成的 echarts 版本为 5.3.2。

## 图表类型

[官方Examples - Apache ECharts](https://echarts.apache.org/examples/zh/index.html)

![image.png](https://cdn.pkmer.cn/images/202307110910064.png!pkmer)

除了官方给的示例代码外下面社区也有大量的范例可供参考：

- [数据可视化技术分享-echarts热门组件 - Powered by Discuz!](http://192.144.199.210/forum.php?mod=forumdisplay&fid=2)
- [DataInsight](http://analysis.datains.cn/finance-admin/index.html#/chartLib/all)
- [PPChart - 让图表更简单](http://ppchart.com/#/)
- [首页 - ECharts Demo集,echarts gallery社区,Make A Pie,分享你的可视化作品isqqw.com](https://www.isqqw.com/)
- [series-bar柱状图 - makeapie echarts图表可视化案例](https://www.makeapie.cn/echarts_category/series-bar)
- [首页 - Made A Pie](https://madeapie.com/#/)
- [MCChart (zhangmuchen.top)](http://echarts.zhangmuchen.top/#/index)
- [全网echarts案例资源大总结和echarts的高效使用技巧（细节版） - 掘金 (juejin.cn)](https://juejin.cn/post/7078834647005822983)

## 使用方法

下面教程针对高级使用者，在编写 dataviewjs 代码时给予参考。后面给出新手直接可以用的代码。

### 点击事件绑定

通过在源数据添加下面字段绑定点击事件效果。 目前支持的类型有 tag，content，file，path 指定这类类型可以点击事件调用 Obsidian Search operators 如果指定的是 file 和 path 类型 需要添加字段比如 data['file']='filename' 可以实现组合搜索 假设 datas 是要展示的数据。

```
datas.forEach((data)=>{
	data['search']='tag'
	data['file']='filename'
	data['path']='path'
})
```

**如果不指定，默认绑定的是传入的 data 数组中的 index 对应的文件。** **If not specified, the default binding is to the file with index in the incoming data array. **

### 渲染容器

将下方代码到 option 选项后即可渲染 Render the code below after putting it into the option

```
app.plugins.plugins['obsidian-echarts'].render(option, this.container)
```

## 举例

### 一个简单的柱状图案例

教你如何把官方示例用到 obsidian 中。

比如这个简单的柱状图示例，[Examples - Apache ECharts](https://echarts.apache.org/examples/zh/editor.html?c=bar-simple&lang=ts)

把左边的代码复制到笔记的代码块中

![image.png](https://cdn.pkmer.cn/images/202307110951253.png!pkmer)

代码的意思就是 定义了 x 轴，y 轴的属性，和序列对应的值。

官方给的例子数据都是定义好的，人为的输入进去的，这在实际应用中是不现实的，所以需要借助 dataview 工具帮我们筛选需要的数据进去。

现在我们假设库里有一堆笔记，标签都是 movie，yaml 区域有很多笔记属性 比如

![image.png](https://cdn.pkmer.cn/images/202307110955590.png!pkmer)

现在我需要把 Movie 标签的笔记全部收集过来，然后柱状图展示每个笔记的 rating 评分情况。

我们先用 dataviewjs 实现这个需求。把标签为 movie 的笔记并且含有 rating 字段的笔记全部列出来。

````
<pre class="dataview dataview-error">Dataview JS queries are disabled. You can enable them in the Dataview settings.</pre>
````

现在会把符号要求的文件属性全部列出来

![image.png](https://cdn.pkmer.cn/images/202307111049087.png!pkmer)

我们只需要文件名和 rating 评分这两个属性 于是继续这样写

创建两个数组 ratingList 用来收集评分。fileList 用来收集文件名。

```
const ratingList = []
const fileList = []
pages.forEach((page)=>{
	fileList.push(page.name)
	ratingList.push(page.rating)
})
```

有这两个数组 就按官方示例把对应的内容替换下

![image.png](https://cdn.pkmer.cn/images/202307111053640.png!pkmer)

替换后 最后加上一句

`app.plugins.plugins['obsidian-echarts'].render(option, this.container)` 意思是把 option 的内容推送到 obsidian-echarts 插件去渲染。

完整代码如下：

````yaml

<pre class="dataview dataview-error">Dataview JS queries are disabled. You can enable them in the Dataview settings.</pre>
````

最后的效果

![image.png](https://cdn.pkmer.cn/images/202307111057033.png!pkmer)

可以看出 x 轴很多文件名不显示应该是因为文件名太长，显示不下，于是稍微改下代码让文件名斜着显示。

在 x 轴添加代码 ` axisLabel: {rotate: 30},`

![image.png](https://cdn.pkmer.cn/images/202307111100302.png!pkmer)

最后效果如下

![image.png](https://cdn.pkmer.cn/images/202307111100417.png!pkmer)

### 动态显示笔记大小和数量分布

![171559841-cfa4e5e2-69be-4506-a32f-beac33842052.gif](https://cdn.pkmer.cn/images/202307110917093.gif!pkmer)

dataviewjs 代码：

````yaml
<pre class="dataview dataview-error">Dataview JS queries are disabled. You can enable them in the Dataview settings.</pre>
````

### 词云

可以把库中出现的关键词用词云标识，这里以查询库中文件所用的标签，形成标签词云为例。

![image.png](https://cdn.pkmer.cn/images/202307110927994.png!pkmer)

````yaml
<pre class="dataview dataview-error">Dataview JS queries are disabled. You can enable them in the Dataview settings.</pre>

````

### 扇形图

这里通过统计库中所有文件形成笔记数量的分布图

![image.png](https://cdn.pkmer.cn/images/202307110932295.png!pkmer)

````yaml

<pre class="dataview dataview-error">Dataview JS queries are disabled. You can enable them in the Dataview settings.</pre>
````

### 柱状图

 筛选库中 Movie 这个标签下的所有文件，按笔记中 rating 字段的值作为数据源。点击柱状图的笔记是可以直接跳转到对应笔记的。

![image.png](https://cdn.pkmer.cn/images/202307110936251.png!pkmer)

````yaml
<pre class="dataview dataview-error">Dataview JS queries are disabled. You can enable them in the Dataview settings.</pre>

````