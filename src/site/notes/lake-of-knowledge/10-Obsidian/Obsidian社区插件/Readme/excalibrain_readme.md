---
{"uid":2023080322175606,"title":"Obsidian 插件：ExcaliBrain","tags":["思维导图","效率","文件管理","界面相关","编辑工具","obsidian插件","readme"],"description":"ExcaliBrain 的灵感来自 TheBrain 和 Breadcrumbs。让 Obsidian 具有交互式结构化思维导图，通过解释您的 Markdown 文件中的链接、数据视图字段、标签和 YAML 前端内容而生成。","author":"AI","type":"readme","draft":false,"editable":false,"modified":20230101000000,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/readme/excalibrain-readme/","dgPassFrontmatter":true}
---


# Obsidian 插件：ExcaliBrain

> [!Note] 插件名片
> - 插件名称：ExcaliBrain
> - 插件作者：Zsolt Viczian
> - 插件说明：ExcaliBrain 的灵感来自 TheBrain 和 Breadcrumbs。让 Obsidian 具有交互式结构化思维导图，通过解释您的 Markdown 文件中的链接、数据视图字段、标签和 YAML 前端内容而生成。
> - 插件分类：[' 思维导图 ', ' 效率 ', ' 文件管理 ', ' 界面相关 ', ' 编辑工具 ', 'obsidian 插件 ', 'readme']
> - 项目地址：[点我访问](https://github.com/zsviczian/excalibrain)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?excalibrain)

## 概述

ExcaliBrain 的灵感来自 TheBrain 和 Breadcrumbs。让 Obsidian 具有交互式结构化思维导图，通过解释您的 Markdown 文件中的链接、数据视图字段、标签和 YAML 前端内容而生成。

![ExcaliBrain](https://cdn.pkmer.cn/covers/excalibrain.PNG!pkmer)

> [!tip] 原文出处
>
>下面自述文件的来源于 [Readme](https://ghproxy.net/https://raw.githubusercontent.com/zsviczian/excalibrain/master/README.md)
>

---

## Readme(翻译）

下面是 [[excalibrain\|excalibrain]] 插件的自述翻译

ExcaliBrain 受到 [TheBrain](https://www.thebrain.com) 和 [Breadcrumbs](https://github.com/SkepticMystic/breadcrumbs) 的启发。它是一个互动的、结构化的思维导图，根据你的 Obsidian Vault 中的文件夹和文件来生成，通过解释你的 markdown 文件中的链接、dataview 字段、标签和 YAML 前置内容。

ExcaliBrain 区分了 5 种笔记之间的关系：

- 子节点
- 父节点
- 朋友节点
- 其他朋友节点（右侧的横向关系）
- 兄弟节点

关系是基于以下逻辑推导出来的：

- 通过使用 dataview 字段明确定义的关系（例如 `Author:: [[Isaac Asimov]]`）
- 推断出的关系（不使用 dataview 字段）
  - 前向链接被推断为子节点
  - 反向链接被推断为父节点
  - 如果文件相互链接，则它们是朋友节点
  - 父节点的子节点是兄弟节点

# 先决条件

ExcaliBrain 是建立在 [Dataview](https://github.com/blacksmithgu/obsidian-dataview) 和 [Excalidraw](https://github.com/zsviczian/obsidian-excalidraw-plugin) 之上的。您必须安装并启用这两个插件，才能使 ExcaliBrain 正常工作。

ExcaliBrain 经过优化，可以与 [Hover Editor](https://github.com/nothingislost/obsidian-hover-editor) 良好配合使用。

# 视频和额外背景信息

详细步骤说明

YouTube：

[![缩略图](https://user-images.githubusercontent.com/14358394/169708346-9e41289d-9536-43ec-8f70-2d2ad2d369d6.png)](https://youtu.be/gOkniMkDPyM)

![图片](https://user-images.githubusercontent.com/14358394/169708182-0096a714-4c6c-4d81-a8f0-8d2237faa300.png)

## 快速演示

<https://user-images.githubusercontent.com/14358394/166160307-707c787e-b03e-4271-a207-80604c0248d5.mp4>

如何安装

<https://user-images.githubusercontent.com/14358394/166163247-8af788d9-4de3-4b86-9d0c-b62b4d99d76c.mp4>

反馈、问题、想法、问题

请前往 [GitHub](https://github.com/zsviczian/excalibrain/issues) 报告错误或请求改进。

# 表达感谢

如果您喜欢 ExcaliBrain，请通过在 [https://ko-fi/zsolt](https://ko-fi.com/zsolt) 上给我买杯咖啡来支持我的工作和热情。

请还帮忙通过在 Twitter、Reddit 或其他您经常使用的社交媒体平台上分享 ExcaliBrain 插件的信息来传播。

您可以在 Twitter 上找到我 [@zsviczian](https://twitter.com/zsviczian)，在 Discord OMG 上找到我（zsviczian#6093），以及在我的博客 [zsolt.blog](https://zsolt.blog) 上找到我。

[<img style="float:left" src="https://user-images.githubusercontent.com/14358394/115450238-f39e8100-a21b-11eb-89d0-fa4b82cdbce8.png" width="200">](https://ko-fi.com/zsolt)
