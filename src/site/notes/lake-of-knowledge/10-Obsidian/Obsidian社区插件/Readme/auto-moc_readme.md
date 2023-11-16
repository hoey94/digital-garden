---
{"uid":2023080322144080,"title":"Obsidian 插件：AutoMOC","tags":["obsidian插件","readme"],"description":"查找当前笔记中缺失的链接引用，并将它们导入到当前笔记中。","author":"AI","type":"readme","draft":false,"editable":false,"modified":20230101000000,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/readme/auto-moc-readme/","dgPassFrontmatter":true}
---


# Obsidian 插件：AutoMOC

> [!Note] 插件名片
> - 插件名称：AutoMOC
> - 插件作者：Diego Alcantara
> - 插件说明：查找当前笔记中缺失的链接引用，并将它们导入到当前笔记中。
> - 插件分类：['obsidian 插件 ', 'readme']
> - 项目地址：[点我访问](https://github.com/dalcantara7/obsidian-auto-moc)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?auto-moc)

## 概述

查找当前笔记中缺失的链接引用，并将它们导入到当前笔记中。

![AutoMOC](https://cdn.pkmer.cn/covers/auto-moc.gif!pkmer)

> [!tip] 原文出处
>
>下面自述文件的来源于 [Readme](https://ghproxy.net/https://raw.githubusercontent.com/dalcantara7/obsidian-auto-moc/master/README.md)
>

---

## Readme(翻译）

下面是 [[auto-moc\|auto-moc]] 插件的自述翻译

# Obsidian 的 AutoMOC 插件

该插件旨在简化 MOC（Map of Content）的维护过程。

在记录笔记时，人们可能会忘记为新笔记提供与之关联的 MOC 的反向链接。随着时间的推移，这会导致许多纯粹的单向链接。用户可能会忘记将 MOC 链接到许多笔记上。对于那些使用标签对笔记进行分组并希望维护这些笔记的运行列表的用户，也存在类似的问题。

该插件将缺失的链接提及或标记提及导入到当前光标位置的当前笔记中。

简而言之，该插件提供了一种快速的方式，可以链接回给定笔记的所有链接提及或标记提及。

## 使用方法

目前支持两个命令：<br>

1. 基于链接提取笔记

- 插件会检查与当前文件名匹配的链接提及

1. 基于标签提取笔记

- 插件会检查与从模态弹窗中选择的标签匹配的标签提及

* **新功能**：已添加对前置标签的支持

启用此插件后，将光标放置在要添加链接的可编辑的 Markdown 笔记中。

<br>
命令 1 可通过命令面板、键盘快捷键（必须映射）或功能区按钮运行。缺失的链接提及将被添加到当前光标位置的当前笔记中。

![demo](assets/auto-moc-demo.gif)

**注意：** 插件设置中有一个禁用功能区按钮的选项。仍然可以通过使用命令面板或映射的热键来激活插件。

<br>
命令 2 可通过命令面板或键盘快捷键（必须映射），但不能通过功能区按钮运行。它将打开一个模态弹窗，提示输入一个标签。一旦选择了所需的标签，所有具有该标签的笔记将被导入到当前光标位置的当前笔记中。

![demo](assets/modal-demo.gif)

### 前置元数据支持

该插件将检查笔记的前置元数据中是否有别名。如果找到别名，它将使用别名导入笔记，以便链接显示为

```
[[NOTE|ALIAS]]

并在预览模式中显示为

ALIAS
```

**注意：** 您必须使用下面显示的正确的 YAML 前置元数据结构。否则，别名/标签将无法被识别

```
aliases: [alias1, alias2]
tags: tag1, tag2
```

或者

```
aliases:
- alias1
- alias2
tags:
- tag1
- tag2
```

前置元数据标签不需要在前面加上 "#"。在前置元数据标签前加上 "#" 是无效的 YAML 语法，会导致标签无法被识别。

<br>

**新功能：** 该插件现在支持锚点链接（链接到标题）。此选项可在插件设置中找到。当开启时，插件将搜索最接近链接或标签的标题。这是以贪婪的方式进行的。

**注意：** 前置元数据标签不能链接到最近的标题。

已知问题

在创建新的链接或标签时，Obsidian 可能需要一段时间来解析链接/标签。在此期间，新的链接/标签可能对插件不可见，并且插件将报告“未找到新链接”。为了避免这种情况，请在创建新的链接/标签和运行 AutoMOC 插件之间等待几秒钟。

可能存在其他错误。如果您遇到任何问题，请在 GitHub 的问题选项卡下报告。

## 定价

这个插件是免费提供给所有人使用的，但如果你想表示感谢或帮助支持持续开发，请考虑给我买杯咖啡。这将使我的工作继续进行。
