---
{"uid":2023080322181597,"title":"Obsidian 插件：File Include","tags":["obsidian插件","readme"],"description":"在Obsidian的markdown中包含或嵌入文件。","author":"AI","type":"readme","draft":false,"editable":false,"modified":20230101000000,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/readme/file-include-readme/","dgPassFrontmatter":true}
---


# Obsidian 插件：File Include

> [!Note] 插件名片
> - 插件名称：File Include
> - 插件作者：Till Hoffmann
> - 插件说明：在 Obsidian 的 markdown 中包含或嵌入文件。
> - 插件分类：['obsidian 插件 ', 'readme']
> - 项目地址：[点我访问](https://github.com/tillahoffmann/obsidian-file-include)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?file-include)

## 概述

在 Obsidian 的 markdown 中包含或嵌入文件。

![File Include](https://cdn.pkmer.cn/covers/file-include.png!pkmer)

> [!tip] 原文出处
>
>下面自述文件的来源于 [Readme](https://ghproxy.net/https://raw.githubusercontent.com/tillahoffmann/obsidian-file-include/main/README.md)
>

---

## Readme(翻译）

下面是 [[file-include\|file-include]] 插件的自述翻译

![](demo.png)

使用 `include` 代码块在 Obsidian 中包含文件。

~~~
```include
hello.py
```
~~~

```include
hello.py
```

通过在语言后面加上一个空格来添加语法高亮。

~~~
```include python
hello.py
```
~~~

```include python
hello.py
```

路径是相对于 markdown 文件解析的。在路径前加上 `@/` 以相对于 vault 根目录解析。
