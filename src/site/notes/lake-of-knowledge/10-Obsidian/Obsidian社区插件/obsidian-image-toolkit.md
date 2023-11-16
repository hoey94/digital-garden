---
{"uid":20230329145830,"title":"Obsidian 插件：Image toolkit 提供笔记中查看图片的基本操作","tags":["Obsidian","插件","图片","格式调整","image"],"description":"Obsidian 插件：Image toolkit 提供笔记中查看图片的基本操作","author":"OS","type":"other","draft":false,"editable":false,"modified":20230730133521,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/obsidian-image-toolkit/","dgPassFrontmatter":true}
---


# Obsidian 插件：Image toolkit 提供笔记中查看图片的基本操作

## 概述

提供预览模式下「点击查看大图」的功能，不过 Obsidian 会自动调整图片大小，只要是常规尺寸的图片，应该很少会有看不清图片的情况。

> [!Note] 插件名片
>
> - 插件名称：Obsidian Image Toolkit
> - 插件作者：sissilab
> - 插件说明：提供笔记中查看图片的基本操作
> - 插件分类：[' 界面相关 ', ' 图片 ', ' 编辑工具 ', 'obsidian 插件 ']
> - 插件项目地址：[点我跳转](https://github.com/sissilab/obsidian-image-toolkit)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?obsidian-image-toolkit)

## 效果&特性

![image.png](https://cdn.pkmer.cn/images/4890948bde6941fa6509ee8aa6417bf3_MD5.png!pkmer)

- 通过鼠标滚轮或点击工具栏缩放图标来放大或缩小图片
- 通过鼠标拖拽或键盘方向按键（上、下、左、右）来移动图片
- 支持全屏查看图片
- 支持左旋、右旋、x 轴翻转、y 轴翻转图片
- 支持实现图片的颜色反转
- 支持拷贝图片

## 使用

### 普通模式

当你关闭”贴图浏览“模式（将所点击的图片全屏化到屏幕上），将处于**普通模式**。

**浏览规则**

- 当你点击图片后，该图片将会弹出，并且背景为透明遮罩层
- 在同一时间你仅能点击和预览一张图片
- 在普通模式下，你无法编辑、浏览你的笔记，只能预览和操作图片

**图片导航**

- 当前笔记中所有的图片将会被展示在底部，并且你可以切换这些缩略图来放大预览
- 你需要在配置界面开启”展示图片导航“来使用该功能
- 你可以可以设置图片导航的背景色和被选中图片的边框色

**退出普通模式**

- 点击图片以外的其他地方
- 按 Esc

若处于全屏模式，你需要先关闭全屏模式，然后才能离开图片预览界面

**移动图片**

- 直接用鼠标拖动图片
- 按已配置的方向键来移动图片

如果你为图片移动设置了修改键（Ctrl、Alt、Shift），你需要同时按住修改键和方向键来移动图片。

### 贴图模式

当你打开”贴图模式“（将所点击的图片贴到屏幕上），将处于**贴图模式**。

![image.png](https://s1.vika.cn/space/2023/04/28/87d802b7020e4afc8fcc1763074f137d)

**浏览规则**:

- 你可以在同时点击和弹出 1 指 5 张图片
- 相较于普通模式，在贴图模式下点击弹出的图片没有遮罩层的限制
- 在贴图模式下，你可以在预览图片的情况下，同时编辑和浏览你的笔记

**菜单**:

- 当你右击某个弹出的图片时，将会在你光标右侧显示菜单，这些菜单包含的功能有缩放、全屏、刷新、旋转、翻转、拷贝、关闭等。

**退出**:

- 按 Esc 关闭你鼠标所在的图片
- 在菜单中点击”关闭“

**移动图片**:

- 直接用鼠标拖动图片
- 不支持通过方向键来移动图片

> [!Tip] 相关推荐
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-image-caption\|obsidian-image-caption]]：给图片增加说明题注
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-local-images-plus\|obsidian-local-images-plus]]：将你粘贴的网络图片，自定下载到本地并插入到你粘贴的位置
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-file-link\|obsidian-file-link]]：可以很容易地将文件链接添加到笔记中，提供界面化的选择文件
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/mousewheel-image-zoom\|mousewheel-image-zoom]]： 能够通过按住可配置键（默认为左 alt），在编辑/阅读模式下通过滚轮来调节图像的大小