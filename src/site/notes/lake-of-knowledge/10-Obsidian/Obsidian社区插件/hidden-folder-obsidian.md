---
{"uid":20230616204512,"title":"Obsidian 插件：Hidden Folder 快速隐藏文件夹","tags":["Obsidian","插件","隐藏","文件管理"],"description":"Obsidian 插件：Hidden Folder 快速隐藏文件夹","author":"OS","type":"basic","draft":false,"editable":false,"modified":20230705145020,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/hidden-folder-obsidian/","dgPassFrontmatter":true}
---


# Obsidian 插件：Hidden Folder 快速隐藏文件夹

> [!Note] 插件名片
> - 插件名称：Hidden Folder
> - 插件版本：1.0.7
> - 插件作者：ptrsvltns
> - 插件描述：在文件管理器中快速隐藏文件夹
> - 插件项目地址：[点我跳转](https://github.com/ptrsvltns/hidden-folder-obsidian)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?hidden-folder-obsidian)

## 效果&特性

- 通过正则表达式来隐藏 Obsidian 文件管理器中的目录/文件夹

## 使用

- 需要使用插件自带的设置，来完成设定。
- 首先，书写好正则表达式，定义你要隐藏的文件夹
- 其次，开启选项，选择是隐藏这些文件夹，还是恢复已经隐藏的文件夹
![image.png](https://cdn.pkmer.cn/images/20230616211439.png!pkmer)

### 一些简单正则表示方式

- 隐藏文件夹

> `^folder1`

```html
- folder1 <- match
  - folder1
  - folder2
- folder2
  - folder1
  - folder2
```

- 匹配文件中文件名内容

> `abc`

```html
- folder1
  - folder1
    - subabcfolder1 <- match
  - folderabc2 <- match
- folder2
  - foldabcer1 <- match
  - folder2abc <- match
```

- 匹配

> `\/folder$`

```html
- folder1
  - folder1
  - folder2
- folder2
  - folder1 <- match
  - folder2
```

> `\/?folder$`

```html
- folder1 <- match
  - folder1
  - folder2
- folder2
  - folder1 <- match
  - folder2
```

> `folder1\/folder`

```html
- folder1
  - folder1 <- match
  - folder2
- folder2
  - folder1
  - folder2
```

>[!Tip] 关联推荐
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/quick-explorer\|quick-explorer]]：在应用标题栏和笔记标题栏增加面包屑导航功能，提供了笔记和目录快速切换的能力
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/novel-word-count\|novel-word-count]]：在 Obsidian 的文件资源管理器窗格中显示每个文件、文件夹和保险库的字数，以及更多其他信息。
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-collapse-all-plugin\|obsidian-collapse-all-plugin]]：单击对应图标或者使用命令，展开或关闭文件管理器中的文件夹
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/pane-relief\|pane-relief]]：每个窗格的历史记录、用于窗格移动和导航的快捷键等
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/recent-files-obsidian\|recent-files-obsidian]]：显示最近打开的文件列表
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-gallery\|obsidian-gallery]]：让你的笔记变成画廊
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-tagfolder\|obsidian-tagfolder]]：通过笔记中的标签，重新组织所有的笔记
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/chronology\|chronology]]：按照月历模式导航，轻松了解编辑修改锅的笔记内容。
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-show-file-path\|obsidian-show-file-path]]：显示正在编辑的文件所在的路径