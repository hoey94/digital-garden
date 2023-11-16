---
{"uid":20230712165034,"title":"Obsidian 插件：Trash Explorer 可视化管理笔记回收站","tags":["Obsidian","插件","回收站","可视化编辑"],"description":"Obsidian 插件：Trash Explorer 可视化管理笔记回收站，让你可以管理 Obsidian 的 .trash 文件夹（也叫软件回收站），从中恢复和删除文件","author":"OS","type":"basic","draft":false,"editable":false,"modified":20230831175928,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/obsidian-trash-explorer/","dgPassFrontmatter":true}
---


# Obsidian 插件：Trash Explorer 可视化管理笔记回收站

## 概述

日常笔记的过程中难免会遇到文件的操作，诸如合并、删除等，甚至有时候我们也可能一时疏忽误删了一些内容。

当你需要找回这些内容的时候，一般会参考 [[lake-of-knowledge/10-Obsidian/Obsidian基本使用/笔记删除文件\|笔记删除文件]]。如果你设置了使用软件回收站，那么会发生一个问题，就是它的操作不够直观，需要进入到仓库的具体文件夹中（.trash）。

Trash Explorer 就是为了可视化这个操作而诞生的，你可以直接打开回收站面板，从里面操作需要恢复，还是彻底删除的文件。

> [!Note] 插件名片
> - 插件名称：Trash Explorer
> - 插件版本：1.2.0
> - 插件作者：Per Mortensen
> - 插件描述：让你可以管理 Obsidian 的 .trash 文件夹（也叫软件回收站），从中恢复和删除文件
> - 插件分类：[' 文件管理 ', ' 效率 ', 'obsidian 插件 ']
> - 插件项目地址：[点我访问](https://github.com/proog/obsidian-trash-explorer)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?obsidian-trash-explorer)

## 效果&特性

![image.png](https://cdn.pkmer.cn/images/20230712165609.png!pkmer)

## 使用

> [!Warning] 重要
> - 重要提示：此插件仅适用于 Obsidian 中的软件回收站，即设置 ->文件与链接中的 .trash 文件夹。它不能与操作系统垃圾一起工作。
> - 要启用此功能，请打开设置并转到文件和链接，然后将已删除的文件设置为移动到软件回收站。

### 打开回收站面板

- 使用 Ribbon 区图标
	- 该插件的图标是类似垃圾桶的图标
- 使用命令面吧
	- 可以使用 `ctrl+p` 打开命令面板；
	- 检索 trash explorer
- 无论通过命令还是 Ribbon 区域图标，都可以在面板中打开回收站管理面板（默认在左侧边栏打开）

### 基础使用

- 列表
	- 回收站列表中展示的已经删除的笔记或者附件文件
	- 支持按照文件名搜索已经删除的笔记或者附件
- 恢复
	- 点击刷新 restore 图标，恢复内容一般恢复到仓库根目录，无法回到具体文件原有的位置
- 删除
	- 点击删除图标，支持直接删除的笔记或者附件

### 限制

该插件受到 Obsidian 放置垃圾项的限制，因为它无法访问它们的原始位置。特别是父级文件夹结构如何，Obsidian 始终将项目移动到 `.trash` 文件夹的根目录，因此在恢复时不会保留任何父文件夹。例如，将文件 `Recipes/Belgian waffles.md` 放入垃圾箱将把它移动到 `.trash/Belgian waffles.md`，并在恢复时将其移动到存储库的根目录下的 `Belgian waffles.md`。

> [!Warning] 重要
> - 在这个插件里面进行的删除操作，等同于操作系统的删除操作，并不会进入到系统回收站，所以删除请谨慎。

> [!Tip] 相关推荐
>  - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/file-tree-alternative\|file-tree-alternative]]：提供了一个全新的增强型文件管理器
>  - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/quick-explorer\|quick-explorer]]：在应用标题栏和笔记标题栏增加面包屑导航功能，提供了笔记和目录快速切换的能力
>  - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/novel-word-count\|novel-word-count]]：在 Obsidian 的文件资源管理器窗格中显示每个文件、文件夹和保险库的字数，以及更多其他信息。
>  - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-collapse-all-plugin\|obsidian-collapse-all-plugin]]：单击对应图标或者使用命令，展开或关闭文件管理器中的文件夹
>  - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/pane-relief\|pane-relief]]：每个窗格的历史记录、用于窗格移动和导航的快捷键等
>  - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/recent-files-obsidian\|recent-files-obsidian]]：显示最近打开的文件列表
>  - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-gallery\|obsidian-gallery]]：让你的笔记变成画廊
>  - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-tagfolder\|obsidian-tagfolder]]：通过笔记中的标签，重新组织所有的笔记
>  - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/chronology\|chronology]]：按照月历模式导航，轻松了解编辑修改锅的笔记内容。
>  - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/hidden-folder-obsidian\|hidden-folder-obsidian]]：在文件管理器中快速隐藏文件夹
>  - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-show-file-path\|obsidian-show-file-path]]：显示正在编辑的文件所在的路径
>  - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/hidden-folder-obsidian\|hidden-folder-obsidian]]：快速隐藏文件夹
