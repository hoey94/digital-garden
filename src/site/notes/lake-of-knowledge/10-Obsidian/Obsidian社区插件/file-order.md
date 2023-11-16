---
{"uid":20230513222801,"title":"Obsidian 插件：File Order 允许你快速给文件夹和文件排序并添加数字编号","tags":["Obsidian","插件","文件编号","文件排序"],"description":"Obsidian 插件：File Order 允许你快速给文件夹的文件加上数字编号","author":"Bon","type":"other","draft":false,"editable":false,"modified":20230917094842,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/file-order/","dgPassFrontmatter":true}
---


# Obsidian 插件：File Order 允许你快速给文件夹和文件排序并添加数字编号

## 概述

有些人在使用 Obsidian 的时候喜欢用卢曼的技巧给某些文件加上数字序号，用于排序和分类管理（参考杜威十进制）。有些情况下，你可以慢慢地加上这些编号，但是如果你一次要修改十几个甚至更多的文件标题的话，肯定也会觉得苦不堪言，而这个插件就是为了解决这个问题在存在的。

> [!Note] 插件名片
> - 插件名称：File Order
> - 插件作者：Lukas Bach
> - 插件版本：0.0.6
> - 插件说明：允许你快速给文件夹的文件加上数字编号。
> - 插件项目地址：[点我跳转](https://github.com/lukasbach/obsidian-file-order)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?file-order)

## 效果&特性

![image.png](https://cdn.pkmer.cn/images/20230514131555.png!pkmer)

![image.png|460](https://cdn.pkmer.cn/images/20230802185129.png!pkmer)

## 使用

- 在你启用该插件后，你需要到文件浏览器中，右键任意一个文件，你会看到一个新的选项：`Reorder Items`，然后就会出现一个弹窗来让你动态地拖动文件；
- 当你开始拖动任意的文件或者任意的文件夹以后，其与其它同级的文件或文件夹都会出现一个数字前缀，而数字前缀你可以在当前弹窗中，点击右上角的下箭头可以修改：
	- Index Minimum Length：指的是多少位数字，例如 01 或 001 或 0001；
	- Delimiter：指的是分隔符，默认是一个空格；修改后可以得到例如 01-ABCD 的样式；
	- Starting Index：指的是从 0 还是 多少开始算，例如是 00 还是 01 开始算；
- 以上的设置你也可以在插件设置中直接修改，这样就不用每次都修改了；
	- 不过每次你单独修改的会单独应用在当前的文件夹中；
- 最后，你拖动好后，你就可以得到一个数字序列文件列啦

![image.png](https://cdn.pkmer.cn/images/20230514131519.png!pkmer)

> [!tip]
> - 文件列和文件夹列是分开计算的，互不影响；
> - 插件会自动应用上一次的设置，所以不需要每次重新设置；