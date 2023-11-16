---
{"uid":2023080322161684,"title":"Obsidian 插件：Commando","tags":["obsidian插件","readme"],"description":"使用定义的或每次调用的值，使命令可以重复调用。","author":"AI","type":"readme","draft":false,"editable":false,"modified":20230101000000,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/readme/commando-command-repeater-readme/","dgPassFrontmatter":true}
---


# Obsidian 插件：Commando

> [!Note] 插件名片
> - 插件名称：Commando
> - 插件作者：qaptoR
> - 插件说明：使用定义的或每次调用的值，使命令可以重复调用。
> - 插件分类：['obsidian 插件 ', 'readme']
> - 项目地址：[点我访问](https://github.com/qaptoR/Commando)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?commando-command-repeater)

## 概述

使用定义的或每次调用的值，使命令可以重复调用。

> [!tip] 原文出处
>
>下面自述文件的来源于 [Readme](https://ghproxy.net/https://raw.githubusercontent.com/qaptoR/Commando/master/README.md)
>

---

## Readme(翻译）

下面是 [[commando-command-repeater\|commando-command-repeater]] 插件的自述翻译

# Commando 插件

该插件旨在通过启用重复命令迭代来丰富命令使用体验。

例如，当使用“高级表格”社区插件并且您需要将一行向上移动 20 次时，您可以使用 Commando 一次调用命令，并按照您的指示重复 20 次，而不是在侧边栏 GUI 中点击按钮或反复调用命令。

Commando 之所以被命名为这个名字，是因为它让人想起了社区插件“Commander”，该插件可以创建命令宏（也请参见“QuickAdd”）。

Commando 最初也打算启用宏，但我选择接受帮助并分而治之！

因此，将 Commander 视为将军，将 Commando 视为您的插件军队中的前线士兵，帮助您管理您的 PKM。

### 免责声明

使用 Commando 时，您需自行承担风险，并充分了解到并非 Obsidian 或其他插件提供的每个命令都应以此方式运行。

每个命令都是独一无二的，必须仔细考虑如果连续多次运行该命令会产生什么变化。

强烈建议在使用 Commando 之前，将您的保险库纳入版本控制，以防止文件的更改或删除。伴随着强大的功能而来的是巨大的责任。

作为额外的预防措施，在生产或日常保险库中使用之前，建议在测试保险库中预先测试运行 Commando 的任何命令。

### 关于快捷键的特别说明

为了使用 Vim 缓冲区功能，您不能使用插件“Sequence HotKeys”来打开 Commando Palette。

该插件的操作方式会在从调色板选择任何命令之前消耗缓冲区。

相反，建议您在 Obsidian 的快捷键设置中将热键设置为类似\<alt + shift + p\>的方式。

## 特点

- 配备专用的“Commando 调色板”。一条命令搞定一切！
- 使用 vim 数字前缀缓冲区作为迭代计数
- 设置默认的迭代延迟和可选的每次调用延迟覆盖
- 可选的继续迭代提示
- 使用\<Ctrl + c\>立即中断迭代
- 在状态栏中查看 vim 键缓冲区（可选择限制数字前缀缓冲区）！

# Commando 调色板

在操作上与普通的命令调色板几乎相同，但有一个秘密武器：

当 Obsidian 处于 Vim 模式时，Commando 调色板可以使用 vim 数字前缀缓冲区作为命令迭代计数。

一旦选择了一个命令，可以输入以下任意一个：

- \<Enter\> 使用前缀缓冲区和插件设置中的延迟运行命令
- \<Ctrl + Enter\> 如上所述运行命令，每次迭代后暂停并提示模态框以继续
- \<Alt + Enter\> 弹出一个实例设置模态框，选择迭代计数和可选的延迟以进行此次调用

如果关闭了“允许 Vim 模式”插件设置或 Obsidian Vim 模式

- \<Enter\> 弹出一个实例设置模态框，选择迭代计数或延迟以进行此次调用

### 实例设置模态框

选择迭代次数，并可选择此 Commando 实例运行的延迟。

从此模态框中，输入以下任意内容：

- \<Enter\> 使用输入的迭代次数和延迟运行命令，如果为空则使用插件设置中的延迟
- \<Ctrl + Enter\> 如上运行命令，每次迭代后暂停并弹出模态框以继续

### 提示模态框

如果选择了此选项，每次迭代时的提示将提供一个机会，在继续之前评估任何更改。

不过，不用担心，每等待一毫秒都会倒计时延迟计时器，因此等待时间将始终是以下两者中较大的一个：延迟计时器或您等待继续的时间。它们永远不会合并。

从此模态框中，可以通过以下任一方式继续：

- 按下 \<Tab\> 或 \<Enter\>
- 通过鼠标导航离开以更改焦点
- 按下 \<Escape\> 关闭模态框

#### 瞬间中断

如果在大循环计数期间的任何时候决定停止迭代，请键入：

- \<Ctrl + c\> 立即中断循环。

在关闭提示模态框之前按下该键组合也会在模态框关闭时取消循环。

# 设置

- 允许 Vim 模式
- 最大 Vim 缓冲区
- 命令延迟

### 允许 Vim 模式

无论您是否使用 vim 键绑定，您完全可以控制 Commando 是否具有使用数字前缀缓冲区作为弹药的选项。

关闭此选项将简化 Commando 调色板，只需一个选项来运行命令，要求每次调用都使用实例设置模态。

### 最大 Vim 缓冲区

你是否曾经遇到过在使用 vim 快捷键进行动作时，却忘记了已经输入了多少个数字？

别担心了！为了避免用户意外地多次调用命令，vim 的键缓冲区现在可以在状态栏中显示出来。

Commando 更进一步。插件设置允许你设置一个最大的 vim 缓冲区来限制数字前缀的输入，这样你就再也不会再次运行 vim 动作或命令超过 9、99、999 次了！

### 命令延迟

有些命令需要一秒钟的时间来正确执行任务。与其冒险匆忙执行这些命令，可能会导致灾难性的结果，不如设置一个一致的迭代延迟，给每个命令（以及自己）足够的时间来评估变化。
