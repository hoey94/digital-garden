---
{"uid":20230502004305,"title":"Obsidian 插件：Creases 控制不同标题的折叠展开状态","tags":["Obsidian","插件","标题","展开","收起"],"description":"Obsidian 插件：Creases 控制不同标题的折叠展开状态","author":"OS","type":"other","draft":false,"editable":false,"modified":20230905003845,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/creases/","dgPassFrontmatter":true}
---


# Obsidian 插件：Creases 控制不同标题的折叠展开状态

## 概述

如果你经常使用 Obsidian 编辑长内容笔记，并在文章中使用了多个章节标题（H1～H6），为了能够集中注意力，你可能需要将不需要查看的章节收起来，只专注于书写其中某个小节；目前 Obsidian 仅支持手动逐一点击各个要操作的标题。

Creases 插件给 Obsidian 的标题增加折叠和展开的功能。

> [!Note] 插件名片
> - 插件名称：Creases
> - 插件作者：Liam Cain
> - 插件说明：给 Obsidian 的标题增加折叠和展开的功能。
> - 插件项目地址：[点我跳转](https://github.com/liamcain/obsidian-creases)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?creases)

## 效果&特性

![156103767-33f311de-39ac-422d-b8ea-987ea9c63f7b.png](https://cdn.pkmer.cn/images/156103767-33f311de-39ac-422d-b8ea-987ea9c63f7b.png!pkmer)

## 使用

你可以在命令面板中输入 `Crease` 来选择对应的命令：

- 按级别折叠标题 - 折叠正确文档中与给定级别匹配的所有标题（H1 - H6）
- 折叠更多 - 查找并折叠最近的标题或列表项。
- 折叠更少 - 查找并展开最近的标题或列表项。

标题中添加的 `Crease` 标记，在实时预览和阅读模式下，会显示一个衣服的图标，嗯你可以形象理解成，就是我们是否折叠和展开衣服。

### 常用命令

- 切换 Crease（**Toggle Crease**） - 折叠/展开当前所在的部分
- 对当前的折叠进行 Crease（**Crease the current folds**） - 将 Crease 应用于文件中的当前折叠，使用折叠沿着 creases 可轻松返回这些当前折叠。
- 沿 creases 折叠（**Fold along creases**） - 折叠文件中的所有被 Creased 标记的部分
- 去除 creases - 从当前文件中删除所有 Creases 标记

### 扩展支持

- 支持模板：如果您使用模板核心插件，模板中包含的所有 Creases 标记将自动折叠。
- 支持模板生成器：向模板生成器模板中添加 creases 可以使内容自动折叠。

### 标题等级

Creases 还借用了 vim 的“折叠级别”概念。折叠级别是从笔记中当前的折叠推断出来的。如果您将 `## Heading Level 2` 标题折叠起来，减小折叠级别将展开所有顶部标题直到 `# Heading Level 1`。增加折叠级别将展开所有顶部标题直到 ### Heading Level 3。

- 增加标题折叠级别 - 把折叠级别增加 1
- 减少标题折叠级别 - 把折叠级别减少 1

### 设置—折叠行为（Folding）

可以在插件设置 Folding 中设置：编辑器与大纲面板的同步模式。核心插件选项里启用大纲插件后，右侧边栏会出现大纲面板，以显示编辑中笔记的大纲标题。

此设置有三种选项：

- From Editor to outline: 依编辑器为准变动大纲折叠状态。
- Bidirection: 双向同步，大纲面板和编辑可以互相影响。
- None: 不同步，编辑器中的折叠和大纲保持相互独立。

### 设置—折叠行为（Folding）

Crease 标题的折叠行为。

1. 开启新笔记时标题的折叠状态：
- 基于当前折叠状态
- 总是折叠
1. 按照模板创建的文件折叠状态：
- 打开笔记时折叠
- 打开笔记时展开
- 打开笔记时折叠并移除 Crease 记号

## 高级使用

联动模板

**模板支持** - 如果您使用 [[math/Config/Template/template-plugin\|template-plugin]] 核心插件，模板中包含的任何折叠块都将自动折叠。

为您的折叠创建一个“保存状态”

如果您正在处理一份长文档，您可能会在进行操作时折叠部分内容。现在您想在折叠中进行“查找”。糟糕，它找到了匹配项，但是现在您折叠的内容全部展开了。

相反，将您的折叠保存为褶皱：

1. 运行“将当前折叠标记为 _ 褶皱 _”以标记所有当前折叠。
2. 尽情搜索文档，展开而不用担心。
3. 运行“沿褶皱折叠”以恢复所有折叠到之前的状态。
4. _可选_ 现在您回到了理想的文档折纸状态，您可以运行“去除褶皱标记”来消除折痕标记。

### 希望模板中的内容默认折叠起来

无论您使用核心的**Templates**插件还是**Templater**，您可能会发现自己希望某些部分默认折叠起来，因为您不经常查看它们。

1. 在您的模板文件中，只需确保 `%% fold %%` 出现在您希望折叠的标题或列表项的同一行上。您还可以在模板内部运行“Toggle crease”命令，以自动插入折叠线。

您想要折叠文档中的所有“### Level 3 Heading”。

折叠给定深度的所有标题可能是一个繁琐的过程。现在不再是这样了。

1. 只需运行“Toggle fold for H3”。

> [!Tip] 相关推荐
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/lapel\|lapel]]：在标题旁边显示标题等级
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/number-headings-obsidian\|number-headings-obsidian]]：给笔记中的标题自动编号，以及动态目录