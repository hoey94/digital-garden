---
{"uid":20230502083811,"title":"Obsidian 插件：File Tree Alternative 强大的文件管理器","tags":["Obsidian","插件","增强型文件管理器"],"description":"Obsidian 插件：File Tree Alternative 强大的文件管理器","author":"OS","type":"basic","draft":false,"editable":false,"modified":20230914145625,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/file-tree-alternative/","dgPassFrontmatter":true}
---


# Obsidian 插件：File Tree Alternative 强大的文件管理器

## 概述

说到笔记，自然少不了需要组织和管理。Obsidian 的文件管理器，简洁清爽，但是做为后起之秀，难免在一些前辈面前会让新迁移过来的用户感觉到，功能多少有些掣肘，需要一些强化功能。

这时候就需要用到 File Tree Alternative，提供了一个全新的增强型文件管理器。

> [!Note] 插件名片
> - 插件名称：File Tree Alternative Plugin
> - 插件作者：Ozan Tellioglu
> - 插件说明：提供了一个全新的增强型文件管理器
> - 插件分类：[' 界面相关 ', ' 文件管理 ', 'obsidian 插件 ']
> - 插件项目地址：[点我跳转](https://github.com/ozntel/file-tree-alternative)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?file-tree-alternative)

## 效果&特性

![image.png](https://cdn.pkmer.cn/images/20230502084747.png!pkmer)

## 使用

这是一个全新的增强文件管理器，并不是简单在原有文件管理器上做得修改。所以需要你点击使用新的面板图标，才可以看到效果。

### 通用设置

- 提供一个独立的全新的文件管理器
- 提供类似 Evernote 文件管理视图，同时显示文件夹和文件列表两个面板，支持水平或垂直分割方式排布方式，或关闭此功能，点击文件夹后，整个列表会直接进入到文件夹。在设置中 `Evernote View` 中选择。
- 可以使用 Ribbon 图标激活“文件树叶”（File Tree Leaf），以防出现意外关闭的情况。可以在插件设置中关闭 Ribbon 图标。

### 文件夹面板特性（Folder Pane Features）

- 统计功能：
	- 统计开关：在文件夹视图下，可以为文件夹树增加统计功能，打开插件设置中的 `Folder Count` 即可。
	- 统计细节：设置中找到 `Folder Count Details`。如果想统计每个文件夹中笔记的数量，设置为 `number of notes`；如果想统计所有文件的数量，则可以选择 `number of all files`。也可以完全关闭计数功能，设置中找到 Folder Icons 关闭。
- 外观：
	- 文件夹图标外观：可以调整文件夹面板中文件夹的图标样式，设置中找到 `Folder Icons` 即可。提供 Default、Box Icons、IcoMoon Icons、Typicons、Circle GG 多种图标样式。
	- 根目录显示样式：可以在文件树中打开/关闭根目录名字显示。设置中找到 `Show Root Folder`
- 折叠展开：
	- 可以使用顶部的导航栏，展开/折叠所有文件夹。
- 文件夹聚焦功能：
	- 可以聚焦于某个文件夹，特别适合较多文档和目录层级时候，节省有限展示空间，也可以让你更聚精会神的管理好当前目录结构。
	- 插件会记住上次展开的文件夹和聚焦的文件夹状态，在下次启动时可以加载。

### 文件面板特性（File List Pane Features）

- 列出所有笔记和子文件夹列表，需要打开 `files under sub-folders`。如果您只想查看所选文件夹中的笔记，则可以从插件设置中关闭此选项。也可以从插件设置中打开切换按钮，以切换子文件夹中的的显示。您还可以切换在文件夹下查看笔记和所有文件。
- 文件聚焦聚焦功能：
	- 置顶文件：可以将最喜欢的文件固定在顶部。`Pin to Top`
	- 收藏文件（star/unstar）：这个需要你启用核心插件 - 星标，此功能和核心插件联动。
- 文件搜索：
	- 可以使用全部：搜索所有文件夹，而不是活动文件夹。
	- 可以使用标签：语法与标签搜索文件。它将显示具有完整或部分匹配的所有文件。

### 除外设定

- 排除文件夹：可以在插件设置中定义某些文件夹路径，以将其从主文件夹列表中排除，注意：所有子文件夹都将被排除在外。
- 排除文件：可以在插件设置中定义某些文件扩展名，以在文件资源管理器中排除列表，注意：这类型的文件都将被排除。

### 样式设定

2.3.2 版本后，该插件已经直至自定义样式，而且已经将部分自定义内置，想要取微调这些样式，需要安装 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-style-settings\|obsidian-style-settings]] 插件，并参考对应文档。

#### 示例图片

- 单文件夹视图：

      <img src="https://github.com/ozntel/file-tree-alternative/raw/main/images/folders-view.png" style="width: 400px;" />

- 置顶固定：

      <img src="https://github.com/ozntel/file-tree-alternative/raw/main/images/files-pinned.png" style="width: 400px;" />

>[!Tip] 关联推荐
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/quick-explorer\|quick-explorer]]：在应用标题栏和笔记标题栏增加面包屑导航功能，提供了笔记和目录快速切换的能力
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/novel-word-count\|novel-word-count]]：在 Obsidian 的文件资源管理器窗格中显示每个文件、文件夹和保险库的字数，以及更多其他信息。
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-collapse-all-plugin\|obsidian-collapse-all-plugin]]：单击对应图标或者使用命令，展开或关闭文件管理器中的文件夹
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/pane-relief\|pane-relief]]：每个窗格的历史记录、用于窗格移动和导航的快捷键等
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/recent-files-obsidian\|recent-files-obsidian]]：显示最近打开的文件列表
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-gallery\|obsidian-gallery]]：让你的笔记变成画廊
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-tagfolder\|obsidian-tagfolder]]：通过笔记中的标签，重新组织所有的笔记
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/chronology\|chronology]]：按照月历模式导航，轻松了解编辑修改锅的笔记内容。
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/hidden-folder-obsidian\|hidden-folder-obsidian]]：在文件管理器中快速隐藏文件夹
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-show-file-path\|obsidian-show-file-path]]：显示正在编辑的文件所在的路径
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/hidden-folder-obsidian\|hidden-folder-obsidian]]：快速隐藏文件夹