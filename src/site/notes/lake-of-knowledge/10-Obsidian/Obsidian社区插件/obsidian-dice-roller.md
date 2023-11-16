---
{"uid":20230514013200,"title":"Obsidian 插件：Dice Roller 为你的笔记添加一点随机性","tags":["Obsidian","插件","骰子","随机化","随机性"],"description":"Obsidian 插件：Dice Roller 为你的笔记添加一点随机性","author":"Bon","type":"other","draft":false,"editable":false,"modified":20230603022149,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/obsidian-dice-roller/","dgPassFrontmatter":true}
---


# Obsidian 插件：Dice Roller 为你的笔记添加一点随机性

## 概述

如果你喜欢玩像游戏或者桌游，那么你肯定玩过或者看过，游戏环节或者角色可以获得一些类似骰子的道具，每次摇动骰子都会获得一些特殊效果，甚至有些骰子能改变角色的所有特性；

这种随机性，为输入和编写提供了一定便利性，Dice Roller 插件将骰子加入到了 Obsidian 中。

> [!Note] 插件名片
> - 插件名称：Dice Roller
> - 插件作者：Jeremy Valentine
> - 插件说明：在文档任意地方生成需要随机的内容，这些随机的候选项可以你来定义。
> - 插件项目地址：[点我跳转](https://github.com/javalent/dice-roller)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?obsidian-dice-roller)

## 效果&使用

![Dice roller 0.png](https://cdn.pkmer.cn/images/Dice%20roller%200.png!pkmer)

## 基础使用

正如这个插件名所言，你只需要在安装完插件后，再在文档中任意地方，插入

```
`dice: 1d2`
```

你就可以获得 1 个骰子，2 为最大值（所以你每次只能随机出 1 或 2），如：

![Dice Roller 1.png](https://cdn.pkmer.cn/images/Dice%20Roller%201.png!pkmer)

而如果你用

```
`dice: 4d15`
```

则是 4 个 15 为最大值的骰子的随机值的总和。

而如果你想要更复杂的计算方式，可以随便在里面插入不同的算术，如：

```
`dice: 3d4+3d4-(3d4 * 1d4) - 2^1d7+2333`
```

你会获得对应的随机值。上述就是 Dice Roller 简单而又不失实用的用法了。

接下来将介绍它特殊而又具有独创性的用法。

## Dice Roller 高级用法

即——随机块

虽然说它是高级，但是在 Dice Roller 文档中，它还是和初始用法是视作同类的，它带来了三个非常有用的场景用法。

在文档中任意地方，插入

```
`dice: [[Note]]|paragraph`
```

会返回 Note 标题的段落块——注意，由于代码块在 Obsidian 中也被认为是段落块，所以会直接返回一整个代码块，而代码块现阶段还不会被渲染，如下：

![Dice Roller 2.png](https://cdn.pkmer.cn/images/Dice%20Roller%202.png!pkmer)

类似地，用

```
`dice: [[Note]]|yaml`
```

则返回 YAML 结果。

而如果你想要返回任意一个标签的所有文件中的任意一个块，那么你可以用下边的代码来实现，**需要你先安装了 Dataview**。

```
`dice: #tag`
```

这个会返回所有带有标签的文件的任意一个块。

如我用 `dice: #writings` 就会返回：

![Dice Roller 3.png](https://cdn.pkmer.cn/images/Dice%20Roller%203.png!pkmer)

而当你用

```
`dice: #tag|-`
```

的时候，则会只返回随机一个文件的随机块，类似地，当你用 + 号，则默认为返回每一个。

当然你也可以用这种方式来返回段落块：

```
`dice: #tag|paragraph`
```

或者

```
`dice: #tag|-|paragraph`
```

当然，你还能在这个基础上加上 Dice Roller 的基础参数，例如

```
`dice: 3d[[Note]]|paragraph`
```

可以输出三个 Note 笔记的随机段落块。

到这里，就已经可以介绍我的使用场景了——我不知道第二天做什么菜好要怎么办。

### 看一下第二天做什么菜

由于我的笔记库里面记录了不少之前已经验证过“对我而言”相对简单而又相对好吃的菜的做法。但是由于都是分成一个个笔记的，而这个插件又只能快速引用对应的块，那该咋办呢。

没错，让我们把 Text expand 插件搬出来，不了解这个插件的可以先去看一下我之前写的文章，然后利用它将我所有相关菜聚集成一个文件列表，如下：

![Dice Roller 4.png](https://cdn.pkmer.cn/images/Dice%20Roller%204.png!pkmer)

![Dice Roller 5.png](https://cdn.pkmer.cn/images/Dice%20Roller%205.png!pkmer)

随机菜就会生效，这起码减少了我很多焦虑以及思考时间，虽然有时候还是会觉得很麻烦，但是至少比之前太多选择好。

但是有些人不做饭或者没有选择困难症的，可以忽略这个使用场景，下一个场景可能对于某些人来说更有帮助。

### 今天早上我做点什么

我起床洗漱后有时候会不知道距离出门的三十分钟内，我可以做点什么，而为了解决这个问题，我也加入了对应的随机事件，例如

> 在 Obsidian 上写一篇随想
> 做一下体操
> 看一下今天的科技新闻
> 写一下 Obsidian 快报

而今天我打开日记，就会出现随机事件。

在这个基础上，你就可以思考如果自己放假呢，如果自己周末呢，是不是可以利用这个来配合 Day Planner 来计划一下自己今天想做什么，又是不是可以利用它从自己一直来不及执行的事件中抽一件执行等，然后利用 Dice Roller 来随机化这些事件。

也许会有人问，为什么不能坚持去做一件事，这个我只能说是这些都是我坚持不了的事情，但是我如果隔两天再做其中一件事，那我反而会很有动力，这也是我特别喜欢玩随机的游戏。

不过接下来则是需要你配合自己拆书或者收藏文章的行动，才能模仿的使用场景了。

### 水文章\“洗稿”

就如同上述所讲，你写文章的时候最怕的是没有思路，但是当你想要去模仿别人的思路的时候，你很容易就会被认为是抄袭。

而利用好 Dice Roller 却在一定程度上解决你想不到怎么写的问题，你只要利用上述的标签随机功能，你可以获得一大堆随机块，但是却是基于某个指定主题的，那么你总会能从里面找到一些奇怪的论述方向，如果你觉得不妥，那就继续 Roll ，在思考的过程中同时让 Obsidian 帮你随机一些可能的点子。

但是这个需要你对自己的笔记规划相当合理，而不是每一个笔记随便什么标签都放进去，而且如果你能利用上 Admonition 插件来拆分每一篇文章的区块，那么你又能获得更好的效果了——因为 Dice Roller 支持筛选代码块，而 Admonition 能让你的文本块被整个随机出来。

不过这种方式往往只能用于水文章（用于向上级交代），利用这种方式写的文章很容易有别人的影子，查重率可能 100%（笑）

## 总结

以上是我在用 Dice Roller 插件过程中摸索出的一些对我个人而言很有趣也相当实用的用法，而实现这些用法的功能竟然是 5.0.0 才加入的新功能，所以后续如果我之前介绍的插件有了某些功能更新，我这边也会考虑再写相关的文章，下一篇将介绍 Obsidian 中的两大地图插件—— Obsidian Leaflet 和 MapView Note，谢谢阅读。