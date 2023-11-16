---
{"uid":20230723144341,"title":"Dataview 支持的 Function 函数","tags":["obsidian","插件","dataview","语法","function"],"description":"基本语法学习指南，Function 函数","author":"Huajin,PKMer","type":"other","draft":false,"editable":false,"modified":20231002150451,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/dataview/dataview/30-function/","dgPassFrontmatter":true}
---


# Dataview 支持的 Function 函数

Dataview 提供了一些函数让我们对查询的结果做进一步处理，你可以在除了 From 以外的地方使用。

Datview 提供了非常丰富的函数让我们处理数据，这些函数主要有五类。正文只对函数作大致介绍，可以点击链接查看对应函数的具体用法，我们提供了中文的解释。也可以自行在官方英文文档查看（ [Functions - Dataview](https://blacksmithgu.github.io/obsidian-dataview/reference/functions/#utility-functions) ）

- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/31 - Dataview 中的构造函数\|构造函数]]：这类函数用于将输入值转换为其他数据类型，也就是强制类型转换（11 个）；
- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/32 - Dataview 中的数值运算函数\|数值运算函数]]：这类函数对数值进行各种运算（8 个）；
- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/33 - Dataview 中的对象操纵函数\|对象操纵函数]]：这类函数用于操作对象内部的值（14 个）；
- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/34 - Dataview 中的字符串操纵函数\|字符串操纵函数]]：这类函数专门用于处理字符串（13 个）；
- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/35 - Dataview 中的实用函数\|实用函数]]：一些实用的函数（7 个）；

## 关于函数的一点基础知识

首先我们要知道什么是函数？没有编程基础的人可能会有这个疑问。其实代码的函数演化自数学上的函数。数学上的函数是一种映射关系，给定一个输入值 x，在函数 f 的作用下把这个值映射成另一个值 $y=f(x)$，在这里也一样。例如函数 `sum(...)` 就是 f，输入值 x 是括号里的值，输出值是他们的和，sum(1,2) 会输出 3；

📌 Dataview 的函数由两部分组成：`函数名(输入值)`，对于一个函数我们需要知道：

- 他的函数名是什么，**有没有具体的意思方便记忆**？
- 我们需要给这个函数输入什么，**需要输入几个数据，他们的顺序是什么，输入值的数据类型是什么**？
- 我们输入了数据经过函数的处理，**会不会有返回值，如果有返回值，返回值的数据类型是什么**？

> [!NOTE] 关于返回值
> 返回值也就是函数处理后的结果，那为什么不直接称为结果呢，不是更好理解吗。这其实是因为，在开发函数的时候，需要用一个关键字来标识我们函数的结果是什么，大部分编程语言用的关键字都是 `return ..`，翻译成中文也就是返回值。这个称呼比直接叫结果多了一分动态的感觉，更能体现代码动态执行的状态。

## 函数向量化

大多数函数平常只接受一个输入值并给出一个返回值，如果要处理多个输入值就要重复使用。为了提高效率，我们可以把输入值写成一个 list 列表，函数作用于列表时就是作用于列表中的每一个值，此时函数的返回值也会是一个列表，这就叫函数向量化。

下面分别演示单个输入值的向量化和多个输入值的向量化

```
lower("YES") = "yes"
lower(["YES", "NO"]) = ["yes", "no"]

replace("yes", "e", "a") = "yas" 
replace(["yes", "ree"], "e", "a") = ["yas", "raa"]
```

`lower()` 的输入值是字符串，它的作用是把输入值全部小写然后返回；

`replace()` 有三个输入值，都是字符串。它的作用是把第一个输入值的所有等于第二个输入值的部分都替换成第三个输入值；

## 一、构造函数

这类函数用于将输入值转换为其他数据类型，也就是强制类型转换（11 个）

- object(key1, value1, ...)：利用给定键值对构造对象；
- list(value1, value2, ...)：利用给定值构造列表；
- date(any)：构造时间；
- date(text, format)：构造具有特定格式的时间；
- dur(any)：构造定长时间；
- number(string)：根据字符串构造数字；
- string(any)：构造字符串；
- link(path, [display])：构造链接；
- embed(link, [embed?])：把链接嵌入查询结果中；
- elink(url, [display])：构造网络链接；
- typeof(any)：查询数据类型；
{ #528a53}


## 二、数值操纵函数

这类函数用于操纵数字（8 个）

- round(number, [digits])：向上取整；
- min(a, b, ...)：求最小值；
- max(a, b, ...)：求最大值；
- sum(array)：求和；
- product(array)：
- average(array)：求算术平均值；
- minby(array, function)：根据某种规则（函数）求最小值；
- maxby(array, function)：根据某种规则（函数）求最大值；

## 三、对象操纵函数

这类函数用于操作对象内部的值（14 个）

- contains() 函数及其近似函数 icontains() 和 econtains()：判断是否包含某值；
- containsword：判断是否包含某值；
- extract(obj, key1, key2, ...)：用 obj 中的某些属性作为属性构造新的对象；
- sort(list)：排序列表；
- reverse(list)：翻转列表；
- length(array/object)：求长度；
- nonnull(array)：去掉数组中的所有 null 值（空值）；
- all(array)：当数组中所有元素都是真时返回 true；
- any(array)：当数组中存在真时返回 true；
- none(array)：当数组中没有真时返回 true；
- join(array, [delimiter])：把 array 组合成一个 string，并且第二个输入值作为分隔符（可以不给）；
- filter(array, predicate)：筛选器，满足 predicate 条件的被保留；
- map(array, func)：对 array 中的所有元素用函数 func 做映射；
- flat(array, [depth])：把不同级别的列表组合成一个同级的列表；

## 四、字符串操纵函数

这类函数专门用于处理字符串（13 个）

- regextest(pattern, string)：检查是否可以在字符串中找到给定的正则表达式模式；
- regexmatch(pattern, string)：检查整个字符串是否与给定的正则表达式模式匹配（regextest 匹配部分文本）；
- regexreplace(string, pattern, replacement)：替换字符串中所有匹配正则表达式的部分；
- replace(string, pattern, replacement)：替换字符串中所有与 pattern 相同的部分；
- lower(string)：字符串全部小写；
- upper(string)：字符串全部大写；
- split(string, delimiter, [limit])：在给定的分隔符处分割字符串，可以限制分割次数；
- startswith(string, suffix)：检查字符串是否以某字符串开头；
- endsswith(string, suffix)：检查字符串是否以某字符串结尾；
- padleft(string, length, [padding])：在开头添加给定的字符（默认为空格），使得字符串达到给定的长度
- padright(string, length, [padding])：在结尾添加给定的字符（默认为空格），使得字符串达到给定的长度
- substring(string, start, [end])：字符串切片，取字符串中从 start 到 end（start 从 0 开始）的子串；
- truncate(string, length, [suffix])：截取字符串的开头，并且为截取的字符串增加一个结尾（默认为...）；

## 五、实用函数

- default(field, value)：设置默认值，即当查询的字段为 null （空值），则显示默认值 value ；
- choice(bool, left, right)：就是 if 判断，bool 判断为真时返回 left，否则返回 right；
- striptime(date)：去掉时分秒的信息，只保留日期部分（年月日）；
- dateformat(date, string)：把时间按照 string 给出的 [格式](https://momentjs.com/docs/#/displaying/format/) 输出；
- durationformat(duration, string)：把定长时间按照 string 给出的格式输出；
- localtime(date)：将固定时区中的日期转换为当前时区中的日期。
- meta(link)：获取包含链接元数据的对象。我们可以利用 meta 返回的对象的属性获取信息
	- meta(link).display：获取链接显示的文本；
	- meta(link).embed：判断链接是否是嵌入链接，`![[..]]` 会返回 true，`[[.]]` 则返回 false；
	- meta(link).path：获取链接的路径（链接的路径为字符串）；
	- meta(link).subpath：获取链接的子路径。对于指向标题的链接，返回标题的文本。对于指向块的链接，返回块的 ID。否则子路径将为空。这可以用来选择特定标题下的任务（利用任务的 section 属性可以得到指向任务标题的链接）；
	- meta(link).type：获取链接指向的对象的类型，有 “file”, "header" 和 "block"

下一步，我们总结了一些 dataview 中容易犯的错误 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/40 - FAQ-常见问题\|40 - FAQ-常见问题]].