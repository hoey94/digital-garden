---
{"uid":20230927130459,"title":"Dataview 表格简单查询示例","tags":null,"description":null,"author":"Huajin","type":"other","draft":false,"editable":false,"modified":20230927130518,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/dataview/dataview/dataview/","dgPassFrontmatter":true}
---


# Dataview 表格简单查询示例

**用表格展示 games 文件夹中的所有文件**
`````示例代码
| File |
| ---- |

{ .block-language-dataview}
`````

**用表格列出所有具有 #type/book 标签的文件**
`````示例代码
| File |
| ---- |

{ .block-language-dataview}
`````

**用表格列出具有 #dvjs/el 或 #dv/min 标签的文件**
`````示例代码
| File                                                                                                         |
| ------------------------------------------------------------------------------------------------------------ |
| [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview 表格简单查询示例.md\|Dataview 表格简单查询示例]] |

{ .block-language-dataview}
`````

**用表格列出 books 或 games 文件夹中的所有文件**
`````示例代码
| File |
| ---- |

{ .block-language-dataview}
`````

**用表格列出 games 文件夹中具有 #genre/action 标签的所有文件**
`````示例代码
| File |
| ---- |

{ .block-language-dataview}
`````

**列出所有文件**

> [!attention] 注意
> - 这个结果可能会非常的长，这取决于你的库的文件数目。dataview 更新后过长的结果并不会让你的 obsidian 变得卡顿，可以放心尝试。
> - 如果实在担心，可以另起一行写上 `limit n` 来限制只展示 n 个结果（n 换成你想展示的结果的个数）；
> - <s>只用 `TABLE` 查询时结尾需要跟一个空格。</s> 在 0.5.57 版本修复了这个 BUG。

`````示例代码
```dataivew
TABLE
```
`````