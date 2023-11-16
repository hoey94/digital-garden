---
{"uid":20230504185734,"title":"Obsidian 插件：Quick Explorer 为标题增加面包屑导航功能","tags":["Obsidian","插件","面包屑导航"],"description":"Obsidian 插件：Quick Explorer 为标题增加面包屑导航功能","author":"OS","type":"other","draft":false,"editable":false,"modified":20230831140228,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/quick-explorer/","dgPassFrontmatter":true}
---


# Obsidian 插件：Quick Explorer 为标题增加面包屑导航功能

## 概述

Obsidian 原有的标题栏导航条只能提供两种简单的功能，快速修改文件标题 和 定位所选目录的在文件管理器中的位置。

但面对我们日益增长的笔记，长目录管理和切换会成为一个痛点。Quick Explorer 很好的模拟了我们常见的面包屑导航功能，提供了笔记和目录快速切换的能力。

> [!Note] 插件名片
> - 插件名称：Quick Explorer
> - 插件作者：PJ Eby
> - 插件说明：在应用标题栏和笔记标题栏增加面包屑导航功能，提供了笔记和目录快速切换的能力
> - 插件分类：[' 界面相关 ', ' 文件管理 ', ' 导航工具 ', 'obsidian 插件 ']
> - 插件项目地址：[点我跳转](https://github.com/pjeby/quick-explorer)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?quick-explorer)

## 效果&特性

![quick-explorer.png](https://cdn.pkmer.cn/images/quick-explorer.png!pkmer)

增加一个面包屑导航，可以每层文件夹或者笔记中进行平层的快速切换，也可以快速跳到具体某个层级中的笔记。

## 使用

- 应用标题栏：
	- 在应用程序的标题栏上增加一个面包屑导航，鼠标点击对应文件夹，或者笔记，会显示同级的文件夹和笔记。
	- 显示的同级文件夹和笔记目录，文件夹和笔记分开显示，菜单上部优先显示文件夹。
- 笔记标题栏：
	- 在笔记的标题栏增加一个面包屑导航，鼠标点击对应文件夹，或者笔记，会显示同级的文件夹和笔记。
	- 点击笔记名称， 依然是快速修改文件名
	- 点击文件夹，显示的同级文件夹目录。
	- 显示的同级文件夹和笔记目录，文件夹和笔记分开显示，菜单上部优先显示文件夹。
- 文件夹：
	- 右键单击以获取任何文件、文件夹或面包屑的完整上下文菜单
	- 如果你同层级的目录或者笔记过多，过长的目录会根据鼠标滑动的位置，跟随滑动以便浏览未显示的目录结构。
	- 文件夹会在右侧显示对应包含的笔记数量
- 笔记：
	- 使用 Ctrl/Cmd + 悬停鼠标以预览文件（如果启用了内置的页面预览插件）
	- 单击以打开文件（使用 Ctrl 或 Cmd 在新窗格中打开）
- 拖拽：
	- 你可以通过从面包屑中拖拽文件夹或者笔记，放到对应位置，以打到移动的目的，但是并不支持你拖拽文件到面包屑到导航中。
- 其他：
	* 输入普通文本可在文件夹（或上下文菜单）中搜索项目名称，并选择下一个匹配项
	* 上、下、Home 和 End 在文件夹或上下文菜单中移动
	* 左右箭头选择父文件夹或子文件夹
	* Enter 选择要打开的项目，Ctrl 或 Cmd + Enter 在新窗格中打开文件
	* 反斜杠（`\`）、“上下文菜单”键或 Alt + Enter 打开所选文件或文件夹的上下文菜单
	* F2 启动当前文件或文件夹的重命名，Shift+F2 开始移动
	* Tab 切换“快速预览”模式：当激活时，将自动显示悬停预览，以便您始终在菜单之外查看它（除非您深入子文件夹，已达到屏幕边缘）。这使得通过向下箭头浏览文件夹的内容变得非常容易。
	* 如果当前文件或文件夹的页面预览处于活动状态，PageUp 和 PageDown 将向上和向下滚动，Ctrl 或 Cmd + Home 或 End 跳转到笔记的开头或结尾。滚动到末尾或开始之前（或在没有活动预览的情况下使用任何这些键）将在列表中将选择项移至下一个或上一个文件/文件夹。

>[!Tip] 提示
>该插件没有设置选项

### 当前限制

* 文件总是按照升序名称排序（使用与文件资源管理器视图相同的排序规则）
* 可以从下拉菜单中拖动某个条目，但无法将任何条目放入其中
* 没有办法配置文件的排序或分组

### 快捷键

- **Browse vault**，打开包含仓库根文件夹的下拉目录结构
- **Browse current folder**，打开包含活动文件所在文件夹的下拉目录结构
- **Go to next file in folder**，打开当前笔记的文件夹中的下一个文件
- **Go to previous file in folder**，打开当前笔记的文件夹中的上一个文件
- **Go to first file in folder**，打开当前文件的文件夹中的第一个文件
- **Go to last file in folder**，打开当前文件的文件夹中的最后一个文件

### 样式设置

插件 0.2.0 版本以后：如果你使用的是 0.16.3 以后的版本，想在应用的标题栏，隐藏面包屑或者仓库的版本和名称信息，则可以使用 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-style-settings\|obsidian-style-settings]] 插件将其关闭。

## 兼容性

- 与 Obsidian 本身
	- 当 Quick Explorer 处于激活状态时，它可能会重新格式化标题栏，以便标准的 Obsidian 应用仓库名和版本号信息出现在右侧，而不是中心，为 Quick Explorer 本身腾出空间。
- 与主题
	- Quick Explorer 使用了 Obsidian 用于突出显示高亮按钮的颜色（你可以理解成外观里面的主题色），这样在大多数主题的浅色和暗色模式下提供足够的对比度，但在某些主题中可能过于明亮或鲜艳。
	- 某些主题尝试隐藏或淡化应用的标题栏，使 Quick Explorer 的 UI 不可见。

>[!Tip] 关联推荐
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