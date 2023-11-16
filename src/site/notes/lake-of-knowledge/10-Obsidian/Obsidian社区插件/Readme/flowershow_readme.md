---
{"uid":2023080322183547,"title":"Obsidian 插件：Flowershow","tags":["obsidian插件","readme"],"description":"直接从你的Obsidian vault中使用Flowershow进行发布。","author":"AI","type":"readme","draft":false,"editable":false,"modified":20230101000000,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/readme/flowershow-readme/","dgPassFrontmatter":true}
---


# Obsidian 插件：Flowershow

> [!Note] 插件名片
> - 插件名称：Flowershow
> - 插件作者：Rufus Pollock
> - 插件说明：直接从你的 Obsidian vault 中使用 Flowershow 进行发布。
> - 插件分类：['obsidian 插件 ', 'readme']
> - 项目地址：[点我访问](https://github.com/datopian/obsidian-flowershow)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?flowershow)

## 概述

直接从你的 Obsidian vault 中使用 Flowershow 进行发布。

> [!tip] 原文出处
>
>下面自述文件的来源于 [Readme](https://ghproxy.net/https://raw.githubusercontent.com/datopian/obsidian-flowershow/main/README.md)
>

---

## Readme(翻译）

下面是 [[flowershow\|flowershow]] 插件的自述翻译

# 🌷 Obsidian 花展插件

Obsidian 花展插件，可直接从您的 Obsidian 保险库中使用 [Flowershow](https://github.com/datopian/flowershow) 进行发布。

## 文档

### 初始设置

1. 首先，您需要一个 GitHub 账户。如果您还没有，请在 [此处](https://github.com/signup) 创建一个。
2. 您还需要一个 Vercel 账户。您可以使用 GitHub 账户在 [此处](https://vercel.com/signup) 注册。
3. 打开 [此存储库](https://github.com/datopian/flowershow)，并在“快速克隆和部署”部分下点击蓝色的“Deploy”按钮。这将打开 Vercel 的“创建 Git 存储库”页面。选择一个名称作为您网站的存储库，并点击“创建”，将模板存储库的副本创建到您的 GitHub 账户并部署到 Vercel。
4. 现在您需要在 GitHub 上创建一个个人访问令牌，以便插件可以向存储库添加/删除注释。在登录 GitHub 的情况下，转到 [此页面](https://github.com/settings/tokens/new?scopes=repo)。正确的设置应该已经应用。如果您不想每隔几个月生成一次，请选择“无到期日”选项。点击“生成令牌”按钮，并复制您在下一页上看到的令牌。
5. 在 Obsidian 中打开 Flowershow 插件设置。填写您的 GitHub 用户名、您在步骤 3 中创建的笔记存储库的名称。最后粘贴您在步骤 4 中创建的令牌。
6. 现在，让我们发布您的第一个笔记！在 Obsidian 中创建一个新的笔记。
7. 按下 Windows/Linux 上的 CTRL+P（Mac 上的 CMD+P）打开命令面板，然后找到“Flowershow: Publish Single Note”命令。按回车键。
8. 转到您的网站 URL，您应该在 [Vercel](https://vercel.com/dashboard) 上找到它。如果还没有显示任何内容，请等待一分钟并刷新。您刚刚创建的带有笔记的 Flowershow 网站现在应该已经运行起来了。

恭喜，您现在拥有自己的免费托管的 Flowershow 网站！

现在，您可以像通常在 Obsidian 中那样添加链接，使用双方括号，例如：[[Some Other Note\|Some Other Note]]，链接到您刚刚发布的笔记。您还可以使用语法 [[Some Other Note#A Header\|Some Other Note#A Header]] 链接到特定的标题。请记住，您还需要发布您链接到的笔记，因为这不会自动发生。

### 命令

* `Flowershow: 发布单个笔记` - 将当前笔记发布到您的 Flowershow 网站。
* `Flowershow: 发布所有笔记` - 将您的保险库中的所有笔记发布到您的 Flowershow 网站。

### Ribbon commands

安装插件后，您将在 Obsidian 功能区中看到一个新的图标 - 🌱。

单击它将弹出“发布状态”面板，其中包括：

* **已发布**：已发布到您的 Flowershow 网站的笔记总数
* **已更改**：已在本地编辑的 __ 已发布 __ 笔记的总数（+ 按钮以发布它们）
* **未发布**：在您的 Obsidian 保险库中尚未发布到您的网站的新笔记的总数（+ 按钮以发布它们）
* **已删除**：已从您的 Obsidian 保险库中删除但仍在您的网站上发布的笔记的总数（+ 按钮以取消发布它们）

### 前置设置

* `isDraft` - 设置为 `true` 以使笔记在您的 Flowershow 网站上保持未发布状态（或者如果之前已发布，则取消发布）。默认值：`false`。

开发

### 本地测试

1. 克隆存储库。
2. 运行 `npm i` 安装依赖项。
3. 运行 `npm run build`。
4. 在 Obsidian 插件文件夹中创建到 `main.js`、`manifest.json` 和 `styles.css` 文件的符号链接：

``` sh
ln -s /path/to/obsidian-flowershow/main.js /path/to/obsidian-vault/.obsidian/plugins/flowershow/main.js
ln -s /path/to/obsidian-flowershow/manifest.json /path/to/obsidian-vault/.obsidian/plugins/flowershow/manifest.json
ln -s /path/to/obsidian-flowershow/styles.css /path/to/obsidian-vault/.obsidian/plugins/flowershow/styles.css
```

1. 重新加载 Obsidian，转到设置 > 社区插件，并启用插件。

### 在更改后重新构建

如果您希望在对源代码进行任何更改后自动重新构建插件，请运行 `npm run dev` 而不是 `npm run build`。这将启动一个服务器，它将监视源文件的更改并自动重新构建插件。然而，您仍然需要手动重新加载 Obsidian 以查看更改。

### 热重载

如果你想要真正的热重载，即不需要禁用/启用插件：

1. 安装 [Hot-Reload](https://github.com/pjeby/hot-reload) 插件：
  - 从最新版本中下载 .zip 文件
  - 将 .zip 文件解压到 Obsidian vault 的 `.obsidian/plugins` 文件夹中
  - 进入设置 > 社区插件，启用该插件
1. 不要像上面第 4 步那样创建符号链接，直接将插件文件复制到 Obsidian vault 的 `.obsidian/plugins` 文件夹中：

``` sh
mv /path/to/obsidian-flowershow /path/to/obsidian-vault/.obsidian/plugins/
```

1. 运行 `npm run dev` 启动服务器。

现在，每当你对源代码进行任何更改时，会发生以下两件事情：

1. 插件将自动重新构建。
2. Hot-Reload 插件将检测到插件已被重新构建，并在 Obsidian 中重新加载它。

致谢

非常感谢 [Ole Eskild Steensen](https://github.com/oleeskild) 提供的 [obsidian-digital-garden插件](https://github.com/oleeskild/obsidian-digital-garden/tree/main)，它给了我们灵感，并让我们得以构建。
