---
{"uid":20230504174453,"title":"Obsidian 插件：Obsidian markmind 绘制思维导图、大纲和 PDF 文件标注工具","tags":["Obsidian","插件","思维导图","大纲","PDF","文件标注"],"description":"Obsidian 插件：Obsidian markmind，让你在 Osidian 中绘制思维导图、大纲和 PDF 文件标注工具。包括多种模式，包括导图模式，表格模式，类白板模式。","author":"cuman","type":"other","draft":false,"editable":false,"modified":20230603022359,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/obsidian-enhancing-mindmap/","dgPassFrontmatter":true}
---


# Obsidian 插件：Obsidian markmind 绘制思维导图、大纲和 PDF 文件标注工具

> [!Note] 插件名片
> - 插件名称：Obsidian markmind
> - 插件作者：Mark
> - 插件说明：让你在 Osidian 中绘制思维导图、大纲和 PDF 文件标注工具。包括多种模式，包括导图模式，表格模式，类白板模式。
> - 插件分类：思维导图, PDF
> - 插件项目地址：[点我访问](https://github.com/MarkMindCkm/obsidian-markmind)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?obsidian-enhancing-mindmap)

## 概述

注意此插件并不开源，正常使用免费版本是没问题的。

此插件主要作用就是可以把当前笔记转为思维导图。

| 免费| 支持|
| -------------------- | ------------------------------- |
|  思维导图 basic 模式 |  rich 模式所有功能       |
|  思维导图大纲模式                                    |   pdf 标注                  |
|   `rich` 模式部分功能         |          支持开发者                                      |
|  epub 阅读                                    |   epub 阅读和标注                  |
|  不支持                                    |   导出思维导图为 pdf                      |
|   移动端和电脑端全平台使用        |          移动端和电脑端全平台使用                                      |
|    ￥0         |      ￥80   (永久激活)                                    |
|           |       [购买](https://www.markmind.net/cn)                                        |

## 使用方法

本文介绍主要以免费版本为主。

### 创建 basic 模式思维导图

#### 方法 1

在 markdown 文件中添加 yaml :

 ```yaml
 --- 
mindmap-plugin: basic 
 ---
 ```

在更多菜单中，你可以找到 _打开为思维导图_ 就可以把当前文档转换为思维导图模式。

![basic.e715be2b.gif](https://cdn.pkmer.cn/images/202305041751327.gif!pkmer)

#### 方法 2

在文件夹上右击，点击 _新建思维导图_ 菜单 就可以新建一个思维导图的 md 文件，文件内容自动会添加 yaml 信息。

## 在 markdown 文件中嵌入思维导图

通过使用 `![[mindmap.md]]` 即可嵌入 mindmap 这个思维导图文件。

### 思维导图快捷键

| 新建导图               | Ctrl/Cmd+P                                                |
| ---------------------- | --------------------------------------------------------- |
| 新建节点               | Tab                                                       |
| 新建同级节点           | enter                                                     |
| 删除节点               | Delete/Backspace                                          |
| 编辑节点               | Space/dblclick node                                       |
| 撤销                   | Ctrl/Cmd+Z                                                |
| 恢复                   | Ctrl/Cmd+Y                                                |
| 退出编辑节点           | Tab                                                       |
| 展开节点               | Ctrl/Cmd + /                                              |
| 收缩节点               | Ctrl/Cmd + /                                              |
| 拖放节点               | Drag and drop node                                        |
| 切换焦点节点           | Up/down/left/right                                        |
| 放大、缩小画布         | Ctrl/Cmd + mouse wheel                                    |
| 居中根节点             | Ctrl/Cmd + E                                              |
| 切换导图布局           | 选中某节点 ，Ctrl/Cmd + U / D / L / R / M / J / K / T / Q |
| 删除归纳、外框、联系线 | Delete/Backspace                                          |

>[!Tip] 关联推荐
>- [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-mindmap-nextgen\|obsidian-mindmap-nextgen]]：用于将笔记预览为 Markmap 思维导图
