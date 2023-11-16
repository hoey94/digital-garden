---
{"uid":20230914144952,"title":"Dataview 语法实战：行内 DQL 示例","tags":["Obsidian","Dataview","示例"],"description":"介绍了 Dataview 的一些基础的 Inline DQL 的使用实例","author":null,"type":"other","draft":false,"editable":false,"modified":20231008001546,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/dataview/dataview/dataview-dql/","dgPassFrontmatter":true}
---


# Dataview 语法实战：行内 DQL 示例

与带有三个反引号的代码块查询不同，行内查询用于笔记的文本、标题中，而不是为它们需要一个孤立的块。行内查询的结果可以随着查询值的改变动态改变。

> [!tip] 行内查询总是只产生一个值。
> 鉴于此，我们无法使用行内查询进行页面收集操作，我们更多的会选择用行内查询来获取一个属性。同时，**查询类型不能在内联查询中使用**，但是我们依旧可以使用 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/24 - 表达式\|表达式]].

> [!warning] 注意
> 使用这种查询时，需要在 Dataview 设置中打开 Enable Inline Queries 设置。

行内 DQL 需要写在行内代码中，适合小范围嵌入元数据使用；

- 以一个等号开头，后面跟需要显示的元数据；
- 如果是当前文件的元数据，用 `this` 指代。如果是别的文件的元数据，用那个文件的链接指代；

## 在文中插入一些表达式

- 插入一些简单的数学式子

```
e ≈ 2.7166666666666663
```

![Dataview 的行内 DQL 示例](https://cdn.pkmer.cn/images/Pasted%20image%2020230914212150.png!pkmer)

- 在文中插入一些日期，比如在你的起始页中你可以加上一些倒计时或者正计时（详见 [[用 Dataview 制作一个倒计时或者正计时列表\|用 Dataview 制作一个倒计时或者正计时列表]]）

```
今天还剩 23466 秒，也就是 391 分钟。
这周还剩 3.2715981249999997 天，也就是 391 分钟。
```

## 在文中插入本文件的元数据

需要借助关键字 `this` 指代本文件，用点运算符指向文件的其他元数据。例如你想在文中某处插入文件的创建时间，你可以这样写

```
创建这篇文件的日期是：2023-11-16T00:00:00.000+08:00.
```

![Dataview 的行内 DQL 示例](https://cdn.pkmer.cn/images/Pasted%20image%2020230914210037.png!pkmer)

如果样式不满意，可以用 DQL 的 `dateformat()` 函数修改修改，例如

```
创建这篇文件的日期是：2023/11/16.
or
创建这篇文件的日期是：2023年11月16日星期四 中国标准时间 00:00.
```

![Dataview 的行内 DQL 示例](https://cdn.pkmer.cn/images/Pasted%20image%2020230914210058.png!pkmer)

我们还可以加一些其他内容，比如加一个倒计时，或者是一个正计时

```
创建这篇文件的日期是：2023/11/16，距离今天已经 `= (date(today) - this.file.cday).day` 天辣！
or
创建这篇文件的日期是：2023/11/16，距离今天已经 `= (date(today) - this.file.cday).day` 天辣！
```

## 在文中插入其他文件的元数据

查询别的文件的元数据：用链接代表那个文件（方括号内的 file 替换成目标文件的文件名）

```
`= [[filename]].file.name`
```

> [!tip] 小技巧：修改行内查询的前缀
> 你可以在 Dataview 设置中的“代码块设置”>“内联查询前缀”中将 = 更改为另一个前缀 (如 dv: 或~)

## 配合 DQL 的函数

前面有提到过配合 `round()` 和 `dateformat()` 使用，还可以考虑一下配合其他的函数，例如利用 `choice()` 的选择输出、利用 `truncat()` 函数截断字符串、利用 `default()` 函数为结果设置一个初始值、利用 `length()` 函数计算数量。

- 利用 `round(), trunc(), dateformat(), default()` 这类函数以及点运算符对结果做修正：

```
今天是 **2023-11-16T00:00:00.000+08:00**，现在的时间是 **17:11**。
```

![Dataview 的行内 DQL 示例](https://cdn.pkmer.cn/images/Pasted%20image%2020230916135258.png!pkmer)

这里用到了 `dateformat()` 函数把我们的时间以 `HH:MM` 的格式显示；

```
这篇笔记已经存在了： PT13M50.907S；
这篇笔记已经存在了： 830.907 秒；
这篇笔记已经存在了： 830.91 秒；
```

![Dataview 的行内 DQL 示例](https://cdn.pkmer.cn/images/Pasted%20image%2020230916140101.png!pkmer)

对比一下直接输出、用点运算符输出和用 `round()` 函数四舍五入的结果，选择自己最需要的使用即可。

- 利用 `choice()` 的选择输出示例：

```
还没达标，加油!🏃‍♂️
```

这段行内查询代码用了一个 choice 函数来检测当前文档中的“步数”属性有没有达标，从而选择性输出文本。

```
今天是工作日，努力工作吧!
```

这段行内查询可以筛选今天是不是周末，如果是周末则告知放松，反之则告知努力工作。

- 利用 `length()` 获得查询结果的个数

我们说过，行内查询只能输出一个查询结果， `length()` 查询的结果通常也是对于一个文件内的。例如你想知道“本月任务”这个文件中所有未完成的任务==的个数==，你可以这样写

```
`=length(filter([[本月任务]].file.tasks, (t) => !t.completed))`
```
