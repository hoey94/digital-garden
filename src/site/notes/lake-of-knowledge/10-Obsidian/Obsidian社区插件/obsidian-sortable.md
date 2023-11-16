---
{"uid":20230430003417,"title":"Obsidian 插件：Sortable 为表格提供简单的排序功能","tags":["Obsidian","插件","表格","排序"],"description":"Obsidian 插件：Sortable 为表格提供简单的排序功能","author":"OS","type":"other","draft":false,"editable":false,"modified":20230914150425,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/obsidian-sortable/","dgPassFrontmatter":true}
---


# Obsidian 插件：Sortable 为表格提供简单的排序功能

## 概述

就是用 Markdown 表格语法，生成的表格，或者使用 Dataview、Obsidian Query Language 等插件生成表格。或许你希望这个表格上有一个简单的排序功能，而不是每次就只能按照生成顺序预览。

> [!Note] 插件名片
> - 插件名称：Sortable
> - 插件作者：Alexandru Dinu
> - 插件说明：提供搜索 Obsidian 设置和插件设置选项的能力
> - 插件分类：[' 表格 ', ' 搜索/排序 ', 'obsidian 插件 ']
> - 插件项目地址：[点我跳转](https://github.com/alexandru-dinu/obsidian-sortable)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?obsidian-sortable)

## 效果&特性

![GIF 2023-5-7 15-25-04.gif](https://cdn.pkmer.cn/images/GIF%202023-5-7%2015-25-04.gif!pkmer)

- 支持的数据类型：数字、字符串、[ISO日期](https://regex101.com/r/RfMAcx/1)。自定义比较函数是路线图的一部分（参见此 [问题](https://github.com/alexandru-dinu/obsidian-sortable/issues/12)）。
- 不会更改 Markdown 源代码。排序是通过重新排列表格行（即 `tr` 元素）来完成的。
- 没有依赖项。

## 使用

- 第一次点击：升序
- 第二次点击：降序
- 第三次点击：恢复默认顺序
- 插件本身不包含任何设置项
### 支持排序的数据类型

- 数字、字符串、ISO 日期
- 自定义比较函数是规划路线的一部分（请参见此 [issue](https://github.com/alexandru-dinu/obsidian-sortable/issues/12)
- 不会修改 Markdown 源代码。通过重新排列表格行（即 tr 元素）进行排序。
- 没有依赖项，不需要你额外再去下载或者安装其他插件。

>[!Tip] 关联推荐
>- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/table-editor-obsidian\|table-editor-obsidian]]：改进了表格导航、格式和操作
>- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-excel-to-markdown-table\|obsidian-excel-to-markdown-table]]：可以将来自 Microsoft Excel、Google Sheets、Apple Numbers 和 LibreOffice Calc 的数据粘贴为 Obsidian 编辑器中的 Markdown 表格。
