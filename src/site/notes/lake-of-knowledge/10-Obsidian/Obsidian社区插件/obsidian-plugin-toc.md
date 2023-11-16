---
{"uid":20230428142959,"title":"Obsidian 插件：Table of content 为你的笔记创建笔记目录","tags":["Obsidian","插件","目录","笔记目录"],"description":"Obsidian 插件：Table of content 为你的笔记创建笔记目录","author":"OS","type":"other","draft":false,"editable":false,"modified":20230603020035,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/obsidian-plugin-toc/","dgPassFrontmatter":true}
---


# Obsidian 插件：Table of content 为你的笔记创建笔记目录

## 概述

这个插件帮助你在笔记中生成对应的目录，为你生成静态目录。

> [!Note] 插件名片
> - 插件名称：Table of content
> - 插件作者：[hipstersmoothie](https://github.com/hipstersmoothie)
> - 插件说明：帮助你在笔记中生成对应的目录
> - 插件项目地址：[点我跳转](https://github.com/hipstersmoothie/obsidian-plugin-toc)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?obsidian-plugin-toc)
> - **优点**：和其他目录插件设计思路对比，这个插件希望目录更加灵活，能够在不同标题等级下，生成目录

>[!Warning] 注意
>- 该插件生成的目录为静态目录，新增的标题并不会自动加入其中，需要你修改笔记后手动触发生成。如果你对此不满意，可以参考并使用这个而插件 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/floating-toc\|floating-toc]]

## 效果&特性

![example.gif](https://cdn.pkmer.cn/images/18f61d9dfd67da3a58e82f3a6aa20bea_MD5.gif!pkmer)

## 使用方法

- 使用 Ctrl/Cmd + P，呼出命令面板。
- 输入 Tabel of Content
![image.png](https://cdn.pkmer.cn/images/caa1621d5c5ea2ac9533b123f9349efb_MD5.png!pkmer)
- `Table of Contents：Create table of contents` ：生成当前标题等级下的目录。
- `Table of Contents：Create table of contents for next heading level`：生成当前标题等级的下一级标题的目录 ：

## 自定义目录样式

如果你希望生成的目录，使用嵌套列表计数（例如：1.1，1.2），将以下 CSS 片段添加到黑曜石中。这将影响您笔记中的所有有序列表。

```CSS
ol {
  counter-reset: item;
}

ol li {
  display: block;
}

ol li:before {
  content: counters(item, ".") ". ";
  counter-increment: item;
  padding-right: 5px;
}
```

> [!Tip] 推荐阅读
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-dynamic-toc\|obsidian-dynamic-toc]]：帮助你在笔记中生成对应的目录
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/floating-toc\|floating-toc]]：在笔记一侧生成悬浮目录，效果近似你在其他在线文档中看到的
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-quiet-outline\|obsidian-quiet-outline]]：增强大纲插件，按需自动展开大纲
