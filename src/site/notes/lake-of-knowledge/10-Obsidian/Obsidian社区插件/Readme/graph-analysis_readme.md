---
{"uid":2023080322192783,"title":"Obsidian 插件：Graph Analysis","tags":["obsidian插件","readme"],"description":"在你的保险箱中使用酷的图形算法发现笔记之间的隐藏联系。","author":"AI","type":"readme","draft":false,"editable":false,"modified":20230101000000,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/readme/graph-analysis-readme/","dgPassFrontmatter":true}
---


# Obsidian 插件：Graph Analysis

> [!Note] 插件名片
> - 插件名称：Graph Analysis
> - 插件作者：SkepticMystic & Emile
> - 插件说明：在你的保险箱中使用酷的图形算法发现笔记之间的隐藏联系。
> - 插件分类：['obsidian 插件 ', 'readme']
> - 项目地址：[点我访问](https://github.com/SkepticMystic/graph-analysis)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?graph-analysis)

## 概述

在你的保险箱中使用酷的图形算法发现笔记之间的隐藏联系。

> [!tip] 原文出处
>
>下面自述文件的来源于 [Readme](https://ghproxy.net/https://raw.githubusercontent.com/SkepticMystic/graph-analysis/master/README.md)
>

---

## Readme(翻译）

下面是 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/graph-analysis\|graph-analysis]] 插件的自述翻译

# 图分析

图分析为 Obsidian 添加了**分析视图**，该视图实现了一组算法，用于计算您的存储库中的笔记之间的有用关系！我们的旗舰算法是**共引**面板，我们将其描述为 _ 二级反向链接面板 _。

图分析视图显示了一个笔记名称和数字的表格，每个数字表示与当前笔记相关的某个图分析算法的值。

例如：

- `[[A]]与[[B]]相似度为0.9`
- `[[A]]与[[B]]连接的概率为0.6`
- `[[A]]与[[B]]共引用了6次`

## 分析类型

图分析目前有 4 种不同的分析类型：

1. 相似性
2. 链接预测
3. 共引用
4. 社区检测

每种类型都实现了不同的算法，用于不同的目的。

### 共引用

共引用计算了两个笔记在同一篇笔记中被引用的次数，并在这两个笔记被紧密引用时给予额外权重。

将共引用视为**二级反向链接**面板：它不仅显示了某个内容的引用位置，还显示了为什么、与谁或与什么一起引用！

例如，如果 `[[C]]` 在其内容中有 `[[A]]` 和 `[[B]]`，那么 `[[A]]` 和 `[[B]]` 的共引用次数将各为一。

每个具有共引用次数大于 0 的笔记都会有一个下拉菜单。在每个下拉菜单中，您可以看到哪个笔记共引用了这两个笔记，并且它们共引用的句子（如果在同一句子中），否则只显示带有另一个链接的句子。

![](https://i.imgur.com/9yspOkN.png)

每日笔记的示例用例

@HEmile 给出了一个使用示例：

> 我经常使用每日笔记，我在其中记录日志并写下当天的新闻。这使得反向链接面板有点无聊：它只显示我在哪些日期写过某个笔记。而共同引用算法则给我展示了更多！例如，`Joe Biden` 笔记告诉我，我通常会与 `Donald Trump` 一起写有关 Biden 的内容。但是，如果我想知道我写过关于 Joe Biden 和 `China` 之间关系的内容，我只需查看共同引用面板并展开关系，就可以看到整个故事！

![](https://i.imgur.com/udPkuV3.png)

#### 视频教程

这个视频提供了一个更长、更深入的概述，解释了为什么共引用是如此有用！

[![观看视频](https://yt-embed.herokuapp.com/embed?v=rK6JVDrGERA)](https://youtu.be/rK6JVDrGERA)

### 相似度

相似度是根据音符在图中的连接程度来衡量两个音符的相似程度（即不考虑音符内容）。目前只实现了 Jaccard 相似度测量方法。

#### Jaccard 相似度

**公式**：

![image](https://user-images.githubusercontent.com/70717676/139872572-93504295-6d29-4722-bdb1-3fbeb7bc22ec.png)

[来源](https://neo4j.com/docs/graph-data-science/current/alpha-algorithms/jaccard/#alpha-algorithms-similarity-jaccard-context)

其中：

- `|x|` 是节点 `x` 的邻居数量（指向或指出的链接）。
- `|x & y|` 是节点 `x` 和 `y` 共同拥有的邻居数量。

### 链接预测

链接预测是根据图中节点的其他连接来衡量两个节点之间应该连接的概率。实现的链接预测算法包括 Adamic Adar 和 Common Neighbours。

#### Adamic Adar

**公式**：

![image](https://user-images.githubusercontent.com/70717676/139873180-c870e072-843c-42a9-83fc-87205b408754.png)

[来源](https://neo4j.com/docs/graph-data-science/current/alpha-algorithms/adamic-adar/)

其中：

- `N(x)` 是节点 `x` 的邻居数量

#### 共同邻居

**公式**：

![image](https://user-images.githubusercontent.com/70717676/139873406-d0542335-3b8c-4d08-8a5b-4510408ebd4e.png)

[来源](https://neo4j.com/docs/graph-data-science/current/alpha-algorithms/common-neighbors/)

其中：

- `N(x)` 是节点 `x` 的邻居数量

### 社区检测

这些算法试图找到相似节点的群组。

#### 标签传播

首先，为每个节点分配一个唯一的标签（即其自己的名称）。然后，查看每个节点的邻居，并将其标签更改为邻居中最常见的标签。

重复此过程 `iterations` 次。

最后，按照它们最后拥有的标签将节点分组显示。

#### 聚类系数

给出了节点 `u` 参与的三角形数量与其可能参与的三角形数量之比：

![image](https://user-images.githubusercontent.com/70717676/140610147-0a05201f-d9c7-4c0c-b423-6bbeeb81253b.png)

## 实用类

图表分析表格（或共引下拉菜单）中的每一行都有一个类别：`analysis-linked` 或 `analysis-not-linked`，表示当前笔记是否与该行中的笔记链接。这使您能够根据其连接性来设置表格行的样式。

例如，您可以使链接的笔记具有较低的不透明度：

```css
tr.analysis-linked {
  opacity: 0.3;
}
```

![image](https://user-images.githubusercontent.com/70717676/139862955-75284ff5-0ced-4548-bf6e-caa353a16fe0.png)

您甚至可以完全隐藏链接的行：

```css
tr.analysis-linked {
  display: none;
}
```

## 设置

在分析视图中，您可以选择不同的 `分析类型` 和这些类型中的不同 `算法`。您可以在插件设置中设置默认的分析类型。

还有隐藏 `无穷大` 和 `零` 值的选项。

![image](https://user-images.githubusercontent.com/70717676/138652879-d8b0e4a7-d70a-44e8-ba3c-67e04f6a8edd.png)

## 算法文档

您可以在 [此处](https://neo4j.com/docs/graph-data-science/current/algorithms/) 阅读有关已实现算法的更多信息，或告诉我们您希望我们添加哪些算法👀。关于共引文献的信息大部分可以在 [Wikipedia](https://en.wikipedia.org/wiki/Co-citation) 上找到。特别是，我们实现了 [共引接近度分析](https://en.wikipedia.org/wiki/Co-citation_Proximity_Analysis) 的变体。

购买我们一杯咖啡

SkepticMystic: [![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/G2G454TZF)

Emile: [![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/Emile)
