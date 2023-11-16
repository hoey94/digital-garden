---
{"uid":20230927130535,"title":"Dataview 表格进阶查询示例","tags":[],"description":null,"author":"Huajin","type":"other","draft":false,"editable":false,"modified":20231007235427,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/dataview/dataview/dataview/","dgPassFrontmatter":true}
---


# Dataview 表格进阶查询示例

### 用表格列出作者 Conrad C 的所有数目

- Conrad C 是人名，所有书籍的笔记都打上了 books 标签

`````示例代码
| File |
| ---- |

{ .block-language-dataview}
`````

### 用表格列出读书笔记以及一些额外信息

- 展示了书的作者，已读页数和总页数。

`````示例代码
| File | author | pagesRead | totalPages |
| ---- | ------ | --------- | ---------- |

{ .block-language-dataview}
`````

![Dataview 表格进阶查询示例](https://cdn.pkmer.cn/images/Pasted%20image%2020230927155703.png!pkmer)

### 用表格列出具有 source 属性的笔记且去除表格第一列

`````示例代码
| source | time | ingredients |
| ------ | ---- | ----------- |

{ .block-language-dataview}
`````

![Dataview 表格进阶查询示例](https://cdn.pkmer.cn/images/Pasted%20image%2020230927155654.png!pkmer)

### 对表格进行分组

- 在这一篇中我们讲了 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview 的 GROUP BY 究竟是怎么工作的\|Dataview 的 GROUP BY 究竟是怎么工作的]].

**将读书笔记按照作者分组**

`````示例代码
| author |
| ------ |

{ .block-language-dataview}
`````

- 第一列会变成 author 而不是对应文件的链接。

![Dataview 表格进阶查询示例](https://cdn.pkmer.cn/images/1695801384832.png!pkmer)

**在前一个的基础上再列出文件的链接和已读页数**

`````示例代码
| author | rows.file.link | rows.pagesRead |
| ------ | -------------- | -------------- |

{ .block-language-dataview}
`````

> [!NOTE] 注意
> 这里用的是 `rows.file.link` 和 `row.pagesRead`，不要忽略了这个 `rows`.

![Dataview 表格进阶查询示例](https://cdn.pkmer.cn/images/Pasted%20image%2020230927155836.png!pkmer)

### 自定义表头

**修改附加列的表头**

`````示例代码
| File | Phone Number | E-Mail |
| ---- | ------------ | ------ |

{ .block-language-dataview}
`````

- 直接用 `AS` 关键字重命名即可；

![Dataview 表格进阶查询示例](https://cdn.pkmer.cn/images/Pasted%20image%2020230927160109.png!pkmer)

**修改第一列默认列的名字**

`````示例代码
| Game | developer | price |
| ---- | --------- | ----- |

{ .block-language-dataview}
`````

- 直接去掉第一列，然后再补上的同时用 `AS` 重命名即可。
- 第一列的属性名是 `file.link`，因此补上用的关键字也是 `file.link`；

![Dataview 表格进阶查询示例](https://cdn.pkmer.cn/images/Pasted%20image%2020230927160147.png!pkmer)

**修改成组后组名所在列的列名**

`````示例代码
| Author | Books |
| ------ | ----- |

{ .block-language-dataview}
`````

- 和上一个的方法一样，去掉然后补上并且重命名；
- 成组后的第一列的属性名是 `key`，因此补上用的关键字也是 `key`；

### 对表格中的结果进行排序

`````示例代码
| File | author |
| ---- | ------ |

{ .block-language-dataview}
`````

![Dataview 表格进阶查询示例](https://cdn.pkmer.cn/images/Pasted%20image%2020230927160404.png!pkmer)

更多的排序可以看 [[Dataveiw 自定义排序进阶操作\|Dataveiw 自定义排序进阶操作]]