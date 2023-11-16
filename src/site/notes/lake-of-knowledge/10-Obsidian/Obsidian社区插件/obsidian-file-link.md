---
{"uid":20230517142910,"title":"Obsidian 插件：Better File Link 图形化插入文件和素材","tags":["Obsidian","插件","可视化编辑","插入","效率"],"description":"Obsidian 插件：Better File Link 图形化插入文件和素材","author":"OS","type":"other","draft":false,"editable":false,"modified":20230911152501,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/obsidian-file-link/","dgPassFrontmatter":true}
---


# Obsidian 插件：Better File Link 图形化插入文件和素材

## 概述

Obsidian 本身提供了很丰富的插件引用和插入方式，[[lake-of-knowledge/02-知识管理基础/Markdown/Markdown#引用类型链接\|Markdown#引用类型链接]]，甚至支持你通过拖拽和复制网络图片方式插入，这些都是为了你方便书写你和组织你的笔记，但是有些同学比较习惯传统的插入菜单模式。

有了 Better File Link 这个插件，你可以很容易地将文件链接添加到笔记中，提供界面化的选择文件。

> [!Note] 插件名片
> - 插件名称：Better File Link
> - 插件作者：Marc Julian Schwarz
> - 插件说明：可以很容易地将文件链接添加到笔记中，提供界面化的选择文件
> - 插件分类：[' 编辑工具 ', ' 图片 ', ' 界面相关 ', 'obsidian 插件 ']
> - 插件项目地址：[点我跳转](https://github.com/marcjulianschwarz/obsidian-file-link)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?obsidian-file-link)

## 效果&特性

![Better File Link](https://cdn.pkmer.cn/covers/obsidian-file-link.PNG!pkmer)

![image.png](https://cdn.pkmer.cn/images/20230517143411.png!pkmer)

- 图形化插入文件
- 添加多个文件时，在每个文件链接之前显示自定义前缀
- 自由切换文件结尾的可见性
- 文件链接应该打开文件还是打开文件所在的文件夹
- 在注释中嵌入文件，而不是仅链接文件

## 使用

- 打开命令面板，带有 `Ctrl/CMD + P`
- 搜索命令“ `Better File Link:Add File Link` ”（添加文件链接）
- 单击“选择文件”
- 现在选择你需要的文件
- 确定是否要通过选择复选框来嵌入文件
- 然后按“添加文件链接”

### 设置

- **List style**（列表样式）
	- 如果你添加多个文件链接，你可以指定在每个文件链接前显示的字符
- **Show File extension**（文件扩展名）
	- 切换是否所有插入文件都显示扩展名
- **Link folder instead of file**（链接文件夹而不是文件）
	- 切换是否链接将不会打开文件，而是将打开文件所在的文件夹
- **Use short links**（插入使用短链接）
	- 切换是否显示插入链接为短链接形式

![image.png](https://cdn.pkmer.cn/images/20230517144515.png!pkmer)

### 支持文件格式

- Markdown: `md`
- Images: `png`, `jpg`, `jpeg`, `gif`, `bmp`, `svg`
- Audio: `mp3`, `webm`, `wav`, `m4a`, `ogg`, `3gp`, `flac`
- Video: `mp4`, `webm`, `ogv`
- PDF: `pdf`

> [!Tip] 相关推荐
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-image-toolkit\|obsidian-image-toolkit]]：提供笔记中查看图片的基本操作
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-image-caption\|obsidian-image-caption]]：给图片增加说明题注
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-local-images-plus\|obsidian-local-images-plus]]：将你粘贴的网络图片，自定下载到本地并插入到你粘贴的位置
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/mousewheel-image-zoom\|mousewheel-image-zoom]]： 能够通过按住可配置键（默认为左 alt），在编辑/阅读模式下通过滚轮来调节图像的大小