---
{"uid":20230329145849,"title":"Obsidian 插件：Clear unused images 快速删除无用的图片","tags":["Obsidian","插件","快速删除","图片处理"],"description":"Obsidian 插件：Clear unused images 快速删除无用的图片","author":"OS","type":"other","draft":false,"editable":false,"modified":20230831175634,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/oz-clear-unused-images/","dgPassFrontmatter":true}
---


# Obsidian 插件：Clear unused images 快速删除无用的图片

## 概述

通过删除标记笔记中不再引用的图像，帮助您保持仓库整洁和占用存储控件的节省。

> [!Note] 插件名片
> - 插件名称：clear unused images
> - 插件作者：Ozan Tellioglu
> - 插件说明：清除笔记中不再使用的图像以节省空间。
> - 插件分类：[' 自动化 ', ' 文件管理 ', ' 图片 ', ' 附件 ', ' 效率 ', 'obsidian 插件 ']
> - 插件项目地址：[点我跳转](https://github.com/ozntel/oz-clear-unused-images-obsidian)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?oz-clear-unused-images)

> [!Warning]
> 对于把 OB 当作图片管理器，或者一些笔记就是图片形式存储的同学。请慎用此插件。

## 效果&特性

- 该插件从所有 Markdown 文档中获取所有的图像链接，并将这些图像与您的金库中可用的所有图像文件进行比较。
- 如果检索的图像文件中的任何一个未在仓库的任何文档中引用，它们将被自动删除。

## 设置

### 删除图片的处理方式

请确保在“清除未使用的图像设置”设置下选择已删除图片放到何处。您有 3 个选项：

- 移动到 Obsidian 的 垃圾回收站（.Trash）。和其他删除的文件混在一起，如果你默认开启删除笔记也是放到 OB 自己的回收站的话。
- 移动到操作系统的回收站。和其他操作系统的删除文件混在一起。
- 直接删除：不经过任何回收站，直接从电脑上删除，你可能无法找回。
    ![Pasted image 20230128175756](https://cdn.pkmer.cn/images/f1837d7771ea3af8844d4827bd1040d6_MD5.png!pkmer)

### 排除文件夹

您可以排除需要扫描期的文件夹，如果你不希望删除这些文件夹内的图片。

- 当需要排除多个文件夹时，可以用“，”分隔。
- 请确保在保险库中提供完整的路径。
    ![Pasted image 20230128175751](https://cdn.pkmer.cn/images/a4a1c29058ee2bc2ae59e85b130216d5_MD5.png!pkmer)

也可以排除上面提供的文件夹路径下的所有子文件夹：

![Pasted image 20230128175818](https://cdn.pkmer.cn/images/a1007c783b8bacac6b31c12a3f21edee_MD5.png!pkmer)

## 使用方法

### 支持的格式

**扫描的图像格式**：jpg、jpeg、png、gif、svg、bmp

### 功能更按钮

1. 开启插件后
2. 从插件设置中激活功能区（Ribbon）图标，并从左侧功能区单击图标以运行清理
   ![Pasted image 20230128175857](https://cdn.pkmer.cn/images/0fcfc4bfb2a022061cd065cdbad9f36f_MD5.png!pkmer)

### 命令面板

1. 打开命令面板（使用 Ctrl/Cmd+P）运行“清除未使用的图像”。【 "Clear Unused Images"】
   ![Pasted image 20230128175938](https://cdn.pkmer.cn/images/30201755cb521b5d57b16f878ae13903_MD5.png!pkmer)

2. 当然你也可以给这个命令增加 快捷键。

### 删除日志

如果你在插件设置中打开了“删除日志”选项，你会看到一个弹出的模式，显示哪些图片从你的数据库中已经删除了。

![Pasted image 20230128180054](https://cdn.pkmer.cn/images/ffa739e449346b4157680143ef4a3a88_MD5.png!pkmer)

- 如果所有图像都被使用了，你将会看到以下通知：

![image.png](https://cdn.pkmer.cn/images/20230831175546.png!pkmer)

> [!Tip] 相关推荐
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/attachment-management\|attachment-management]]：可以基于一些建议规则，自动化归类你笔记中的附件内容
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/find-unlinked-files\|find-unlinked-files]]：遍历整个仓库，搜索没有反向链接的文件。它将创建一个文件，其中包含指向这些未链接文件的链接列表
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/settings-search\|settings-search]]：提供搜索 Obsidian 设置和插件设置选项的能力
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/nl-fast-image-cleaner\|nl-fast-image-cleaner]]：快速删除笔记中图片和引用链接
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-regex-pipeline\|obsidian-regex-pipeline]]：让用户用自定义的正则表达式进行格式化文本的插件，相比 Obsidian 自带的搜索替换，Regex Pipeline 利用正则表达式这个强大的文本处理技术可以执行更复杂的文本操作