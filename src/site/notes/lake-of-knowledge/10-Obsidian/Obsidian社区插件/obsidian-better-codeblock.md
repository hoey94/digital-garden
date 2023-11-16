---
{"uid":20230714114750,"title":"Obsidian 插件:Better CodeBlock 代码块显示增强","tags":["插件","代码块增强"],"description":"在阅读视图中为代码块添加标题、行号和折叠按钮","author":"cuman","type":"basic","draft":false,"editable":false,"modified":20230914160055,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/obsidian-better-codeblock/","dgPassFrontmatter":true}
---


# Obsidian 插件:Better CodeBlock 代码块显示增强

## 概述

Obsidian 的代码块一般无法显示具体行号，虽然通过 css 手段可以 [[lake-of-knowledge/10-Obsidian/Obsidian外观/CSS 片段/Obsidian样式-编辑模式代码块显示行号\|编辑模式下显示代码块行号]]，阅读模式下就需要借助插件实现了。better codeblock 插件就可以在阅读视图中为代码块添加标题、行号和折叠按钮，增强了代码块的显示效果。

> [!Note] 插件名片
> - 插件名称：Better CodeBlock
> - 插件作者：StarGrey
> - 插件说明：在阅读视图中为代码块添加标题、行号和折叠按钮
> - 插件项目地址：[点我访问](https://github.com/stargrey/obsidian-better-codeblock)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?obsidian-better-codeblock)

该插件的大部分代码和灵感来自以下两个插件（感谢他们的贡献），图标来自 Admonition。

- <https://github.com/tadashi-aikawa/obsidian-embedded-code-title>
- <https://github.com/nyable/obsidian-code-block-enhancer>

我将两个插件的代码合并并修改了其中一些功能。

## 插件设置项

![image.png](https://cdn.pkmer.cn/images/202307141200363.png!pkmer)

这里注意的是，排除的语言列表中建议写上 `dataview,dataviewjs` 这样可以避免于 dataview 插件冲突。

## 使用说明

添加标题，高亮等代码后不会立马生效，需要重新打开下文件才能看到效果。

- 用于添加标题 `TI:"your title"` 单击标题即可折叠或展开块。
![image.png](https://cdn.pkmer.cn/images/202307141204009.png!pkmer)

- 用于添加某行高亮显示 比如 `HL:"1,2,3"` `HL:"1-3"`
  ![image.png](https://cdn.pkmer.cn/images/202307141206698.png!pkmer)
如图 2,3,5 行已经高亮了
- 用于设置默认折叠 `"FOLD"`
![72.gif](https://cdn.pkmer.cn/images/202307141244548.gif!pkmer)

### 已知问题

- 有时会出现自动换行错误，可以通过切换预览模式来解决
- PDF 导出不能自动换行
