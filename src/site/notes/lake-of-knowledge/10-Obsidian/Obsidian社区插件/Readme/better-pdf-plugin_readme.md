---
{"uid":2023080322150500,"title":"Obsidian 插件：Better PDF Plugin","tags":["PDF","编辑器","obsidian插件","readme"],"description":"允许你插入、缩放、旋转和裁剪 pdf 页面到您的笔记中。","author":"AI","type":"readme","draft":false,"editable":false,"modified":20230101000000,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/readme/better-pdf-plugin-readme/","dgPassFrontmatter":true}
---


# Obsidian 插件：Better PDF Plugin

> [!Note] 插件名片
> - 插件名称：Better PDF Plugin
> - 插件作者：MSzturc
> - 插件说明：允许你插入、缩放、旋转和裁剪 pdf 页面到您的笔记中。
> - 插件分类：['PDF', ' 编辑器 ', 'obsidian 插件 ', 'readme']
> - 项目地址：[点我访问](https://github.com/MSzturc/obsidian-better-pdf-plugin)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?better-pdf-plugin)

## 概述

允许你插入、缩放、旋转和裁剪 pdf 页面到您的笔记中。

![Better PDF Plugin](https://cdn.pkmer.cn/covers/better-pdf-plugin.gif!pkmer)

> [!tip] 原文出处
>
>下面自述文件的来源于 [Readme](https://ghproxy.net/https://raw.githubusercontent.com/MSzturc/obsidian-better-pdf-plugin/master/README.md)
>

---

## Readme(翻译）

下面是 [[better-pdf-plugin\|better-pdf-plugin]] 插件的自述翻译

Obsidian Better PDF 插件的目标是在 Obsidian 中实现原生的 PDF 处理工作流程。

### 特点

- 在笔记中插入单个 PDF 页面
- 将列表或页面范围插入到 Obsidian 笔记中
- PDF 超链接
- 调整 PDF 页面的大小以适应笔记布局
- 旋转 PDF
- 剪切 PDF 部分

### 演示

![示例](https://github.com/MSzturc/obsidian-better-pdf-plugin/raw/master/sample/BetterPDF.gif)

### 语法

|参数|是否必需|示例|
|--|--|--|
|url|是|**myPDF.pdf** 或 **subfolder/myPDF.pdf** 或 "[[MyFile.pdf\|MyFile.pdf]]"
|link|可选（默认为 false）| **true** 或 **false**
|page|可选（默认为 1）| **1** 或 **[1, [3, 6], 8]** 其中 **[3, 6]** 是包含的页面范围。page = 0 是整个文档的别名
|range|可选| **[1, 3]** 插入页面 **1** 到 **3**（包括）。覆盖 page。
|scale|可选（默认为 1.0）| **0.5** 表示 50% 大小或 **2.0** 表示 200% 大小
|fit|可选（默认为 true）| **true** 或 **false**
|rotation|可选（默认为 0）| **90** 表示 90 度或 **-90** 表示 -90 度或 **180**
|rect|可选（默认为\[0,0,0,0\]）| 偏移量 X，偏移量 Y，大小 Y，大小 X（以像素为单位）

### 集成

- [使用JavaScript为Adobe Acrobat Pro和使用AppleScript为Skim创建必要的Better PDF Plugin代码段](https://github.com/johnsidi/scripts-for-Obsidian-Better-PDF-Plugin)



