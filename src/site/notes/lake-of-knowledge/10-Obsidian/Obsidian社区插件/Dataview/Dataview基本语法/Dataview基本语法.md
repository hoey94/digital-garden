---
{"uid":20230723144352,"title":"Dataview 基本语法学习指南","tags":["Obsidian","插件","数据库","分类","教程","查询"],"description":"Dataview 基本语法学习指南","author":"Huajin,PKMer","type":"basic","draft":false,"editable":false,"modified":20230810175825,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/dataview/dataview/dataview/","dgPassFrontmatter":true}
---


# Dataview 基本语法学习指南

## 食用指南

我们大体介绍 Obsidian Dataview 插件的基本语法，在不学习任何编程的前提下，看完后面罗列的内容。相信你也可以完成内容相关的内容。

Dataview 将 Obsidian Vault 变成了一个数据库，使得我们可以用 DQL (Dataview Query Language) 进行查询。

- 如果没有如何编程经验，推荐按照我们提供的顺序学习 Dataview；
- 如果你有一定数据库的基础，可以直接看 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/10 - Metadata 元数据\|10 - Metadata 元数据]] 以及 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/41 - DQL 与 SQL 的异同\|41 - DQL 与 SQL 的异同]]；
- 如果你已经非常熟悉 Dataview 语法，但是想通过我们提供的例子找一些灵感，可以看我们的示例库；

当然如果你熟悉英文或者能够熟练使用翻译软件，可以同步阅读插件的 [官方教程](https://blacksmithgu.github.io/obsidian-dataview/)，这里有更加权威的教程。

## 结构综述

首先我们先通过一个简单的示例让你对 Dataview 的代码有部分概念，然后学习 Dataview 需要知道的一些预备知识 (Metadata)，之后拆解 Dataview 的代码结构，逐块讲解每一部分的含义，配合我们提供的例子，尽量让读者能够学会如何自己动手写一个 Dataview 代码。

- **0x 部分**：用于帮助入门
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/Dataview基本语法\|Dataview基本语法]]：本指南，可以作为学习本基本语法教程的流程；
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/01 - 简单示例\|01 - 简单示例]]：你可以通过一个简单但是完善的示例来初步了解一下用 Dataview 查询时我们做了什么。

- **1x 部分**：学习 Dataview 之前，你需要知道这些：
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/10 - Metadata 元数据\|10 - Metadata 元数据]]：什么是 Metadata 元数据；
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/11 - 添加元数据至文件\|11 - 添加元数据至文件]]：如何向文件中添加元数据；
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/12 - 添加元数据至列表和任务\|12 - 添加元数据至列表和任务]]：如何向一个列表或者任务添加元数据；
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/13 - Metadata的数据类型\|13 - Metadata的数据类型]]：这里列出了所有元数据的数据类型；
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/14 - 隐式字段\|14 - 隐式字段]]：想知道一篇文件中有哪些已有的元数据么？看这篇就够了；
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/15 - Literals 字面常量\|15 - Literals 字面常量]]：查询中的一些静态常量；

- **2x 部分**：真正开始进入到代码的世界
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/20 - 四种查询方式\|20 - 四种查询方式]]：初步讲述了三种使用 Dataview 查询的方式，分别是行内查询、代码块查询和 dvjs 查询；
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/21 - 查询类型\|21 - 查询类型]]：详细的讲述了 Dataview 提供的四种查询结果的展示类型 List, Table, Calendar 和 Task；
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/22 - 查询字段\|22 - 查询字段]]：查询对象 Field，也就是我们最后想要显示的内容组成的列表；
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/23 - 操作符\|23 - 操作符]]：我们对查找到的内容做的操作（筛选，排序，成组，拆分，限制数量等）；
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/24 - 表达式\|24 - 表达式]]：除了查询类型和操作符以外的所有内容，都是表达式；

- **3x 部分**：我们给所有函数提供了中文解释
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/30 - Function 函数\|30 - Function 函数]]：罗列并描述了所有 Dataview 提供的函数的作用；
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/31 - Dataview 中的构造函数\|31 - Dataview 中的构造函数]]
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/32 - Dataview 中的数值运算函数\|32 - Dataview 中的数值运算函数]]
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/33 - Dataview 中的对象操纵函数\|33 - Dataview 中的对象操纵函数]]
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/34 - Dataview 中的字符串操纵函数\|34 - Dataview 中的字符串操纵函数]]
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/35 - Dataview 中的实用函数\|35 - Dataview 中的实用函数]]

- **4x 部分**：一些补充的内容
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/40 - FAQ-常见问题\|40 - FAQ-常见问题]]：罗列了一些使用 Dataview 中可能出错的地方，如果你在自己上手编写属于自己的查询代码时报错，可以看看是否有你遇到的问题；
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/41 - DQL 与 SQL 的异同\|41 - DQL 与 SQL 的异同]]：列举了一些相同点和不同点；
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/42 - ISO 8601\|42 - ISO 8601]]：详细又不特别深入的讲解一种时间格式；
[[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/43 - YAML 基础\|43 - YAML 基础]]：主要讲了 YAML 的 MAP 和 LIST 内容；