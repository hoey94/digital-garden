---
{"uid":20230925122541,"title":"Dataview 列表进阶查询示例","tags":[],"description":null,"author":"Huajin","type":"other","draft":false,"editable":false,"modified":20230928512423190000,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/dataview/dataview/dataview/","dgPassFrontmatter":true}
---


# Dataview 列表进阶查询示例

文中所有的查询来源于 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview 示例展示检索文章结构\|Dataview 示例展示检索文章结构]]；

### 根据一个确定的作者列出所有书

`````示例代码

{ .block-language-dataview}
`````

### 列出所有具有标签 type/books 的文件并展示作者

> [!attention] 注意❗
> 在列表中，你只能附加一个输出信息（在 Field 区域）。如果想要输出更多的信息，可以考虑用 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/21 - 查询类型\|表格]]，或者用 `+` 运算符拼接想要的输出。

`````示例代码

{ .block-language-dataview}
`````

### 列出所有 food 文件夹中含有 source 属性的文件（不展示文件名）

`````示例代码

{ .block-language-dataview}
`````

### 对列表进行分组

- 在这一篇中我们讲了 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview 的 GROUP BY 究竟是怎么工作的\|Dataview 的 GROUP BY 究竟是怎么工作的]].

`````示例代码

{ .block-language-dataview}
`````

### 对列表的元素进行排序

`````示例代码

{ .block-language-dataview}
`````

> [!hint] Advanced usage
> 更多的 dataview 查询示例请见 [[Dataview 实例展示\|Dataview 实例展示]]
