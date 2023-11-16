---
{"uid":20230723144349,"title":"Dataview 语法实战","tags":["obsidian","dataview","示例","实际教学"],"description":"Dataview 语法实战，实际教学，实战","author":"Huajin,Windysoul,PKMer","type":"other","draft":false,"editable":false,"modified":20231029225015,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/dataview/dataview/dataview/","dgPassFrontmatter":true}
---


# Dataview 语法实战

>[!tips]
> - 使用本库，请务必安装 Obsidian 社区插件 Dataview
> - 安装后请务必启用该插件

不要为了用 dataview 而用 dataview，而是要到需要用 dataview 的时候，再来用。考虑到前面的语法介绍可能有的地方写的不够清晰。故增加这一篇幅，汇总一些基础简单的语法但却能涵盖：

1. **笔记统计和分析**：Dataview 可以帮助你统计和分析笔记的元数据，例如计算总的笔记数量、按标签分组并计数、按时间排序等。这对于笔记整理、知识管理和了解笔记库的内容非常有帮助。
2. **任务管理和待办事项**：通过 Dataview，你可以创建一个任务管理系统，跟踪所有的待办事项和任务。你可以根据标签、日期和状态等属性筛选和排序任务，使任务管理更加轻松高效。
3. **阅读进度追踪**：使用 Dataview 可以追踪你的阅读进度，例如标记已读和未读的笔记，计算已读百分比，或者按照阅读顺序排序笔记等。这对于阅读和学习笔记的管理非常有用。
4. **知识地图和链接分析**：Dataview 可以帮助你创建知识地图，展示笔记之间的链接关系和依赖关系。你可以根据笔记之间的链接关系进行可视化分析，了解和发现不同笔记之间的连接，从而更好地组织和理解知识结构。
5. **项目管理和进度追踪**：通过 Dataview，你可以创建一个项目管理系统，追踪不同项目的进展和状态。可以根据项目名称、负责人、优先级等属性来过滤和排序项目，以便更好地管理和追踪进度。

，旨在你有需求时，可以找到类似的实例，亦或者是在学习 dataview 的时候，遇到不懂的地方可以直接来找已有的使用示例，希望通过具体的实例可以让你对各个函数的理解更加深刻。（如果想看行内查询的示例，可以看 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview语法实战-行内DQL示例\|Dataview语法实战-行内DQL示例]]，本文主要针对代码块查询）

## Part 1 - 按查询类型分类

- 表格形式：TABLE
	- 简单示例：[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview 表格简单查询示例\|Dataview 表格简单查询示例]]；
	- 进阶示例：[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview 表格进阶查询示例\|Dataview 表格进阶查询示例]]；
	- 更多花样：
		- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview社区实践经验/Dataview实战-定制你的数据表格并为表格列添加个性化样式\|Dataview实战-定制你的数据表格并为表格列添加个性化样式]]；
		- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview语法实战-列出特定标题下的元素\|Dataview语法实战-列出特定标题下的元素]]
- 列表形式：LIST
	- 简单示例：[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview 列表简单查询示例\|Dataview 列表简单查询示例]]；
	- 进阶示例：[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview 列表进阶查询示例\|Dataview 列表进阶查询示例]]；
- 任务形式：TASK
	- 简单示例：[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview 任务简单查询示例\|Dataview 任务简单查询示例]]；
	- 进阶示例：[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview 任务进阶查询示例\|Dataview 任务进阶查询示例]]；
- 日历形式：CALENDAR
	- 简单示例：[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview 日历查询示例\|Dataview 日历查询示例]]；

## Part 2 - 按操作符分类

考虑到 LIMIT 比较好理解，暂不提供示例。只注意 DQL 是顺序执行的，LIMIT 放在前面的时候会先减少个数再执行后面的代码；

- SORT：自定义排序的示例
	- 简单示例：[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview语法实战-自定义排序的简单实例\|Dataview语法实战-自定义排序的简单实例]]；
	- 进阶示例：[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview语法实战-自定义排序进阶操作实例\|Dataview语法实战-自定义排序进阶操作实例]]；
- FLATTEN
	- 简单示例：[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview语法实战-FLATTEN操作符入门示例\|FLATTEN 操作符简单示例]]；
	- 进阶示例：[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview语法实战-FLATTEN操作符进阶示例\|FLATTEN 操作符进阶示例]]；
- GROUP BY
	- 简单示例：[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview语法实战-GROUP BY 操作符简单示例\|GROUP BY 操作符简单示例]]；
	- 进阶示例：[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview语法实战-GROUP BY 操作符进阶示例\|GROUP BY 操作符进阶示例]]；
	- 深层剖析：[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview 的 GROUP BY 究竟是怎么工作的\|GROUP BY 究竟是怎么工作的]]；

## Part 3 - 按函数分类

我们常常会在以下场景中使用 Dataview 进行查询：

这些只是 Dataview 插件的一些常见使用场景，你可以根据自己的需求和使用习惯，发现更多适合你的场景，并灵活应用 Dataview 插件来加强 Obsidian 中的数据分析和可视化能力。

- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/31 - Dataview 中的构造函数\|构造函数]]：这类函数用于将输入值转换为其他数据类型，也就是强制类型转换（11 个）；
- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/32 - Dataview 中的数值运算函数\|数值运算函数]]：这类函数用于操纵数字（8 个）；
- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/33 - Dataview 中的对象操纵函数\|对象操纵函数]]：这类函数用于操作对象内部的值（14 个）；
- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/34 - Dataview 中的字符串操纵函数\|字符串操纵函数]]：这类函数专门用于处理字符串（13 个）；
- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/35 - Dataview 中的实用函数\|实用函数]]：一些实用的函数（7 个）；

## Part 4 - 其他使用

我们在这里提供了许多使用 Dataview 的案例供大家直接使用。每篇文章实际上是基于我们的 Vault 中的一个 Example 库，Example 库中的文件的 YAML 区域具有名为==主题==和 ==createdDate== 的元数据。如果想要具体使用到自己的笔记中，需要根据自己的笔记作适当修改，比如修改查询的范围要改成自己的笔记中的范围，把查询的条件根据自己的笔记适当修改等。

- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/添加某一主题笔记列表--表格用法\|添加某一主题笔记列表--表格用法]]
- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/添加某一主题笔记列表--基本用法\|添加某一主题笔记列表--基本用法]]
- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/添加某一主题笔记列表--进阶用法\|添加某一主题笔记列表--进阶用法]]
- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/添加相同主题笔记列表--表格用法\|添加相同主题笔记列表--表格用法]]
- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/添加相同主题笔记列表--基本用法\|添加相同主题笔记列表--基本用法]]
- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/添加相同主题笔记列表--进阶用法\|添加相同主题笔记列表--进阶用法]]
- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/添加相同主题笔记列表--完全相同\|添加相同主题笔记列表--完全相同]]
- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/添加相同主题笔记列表--指定月份\|添加相同主题笔记列表--指定月份]]
- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/汇集主题--关于笔记的创建日期和主题的汇集\|汇集主题--关于笔记的创建日期和主题的汇集]]
