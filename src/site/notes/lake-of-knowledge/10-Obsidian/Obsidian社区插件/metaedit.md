---
{"uid":20230516082453,"title":"Obsidian 插件：Metaedit 不可多得的 YAML 管理器","tags":["Obsidian","插件","编辑工具","效率"],"description":"Obsidian 插件：Metaedit 帮你快捷管理Ob的元数据信息，可以预设 yaml 区域的值，不可多得的 YAML 管理器","author":"cuman","type":"basic","draft":false,"editable":false,"modified":20230604172518,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/metaedit/","dgPassFrontmatter":true}
---


# Obsidian 插件：Metaedit 不可多得的 YAML 管理器

> [!Note] 插件名片
> - 插件名称：MetaEdit
> - 插件作者：Christian B. B. Houmann
> - 插件说明：帮你快捷管理 Obsidian 的元数据，可以预设 YAML 区域的值。
> - 插件分类：编辑工具, 效率
> - 插件项目地址：[点我访问](https://github.com/chhoumann/MetaEdit)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?metaedit)

## 概述

Metaedit 是 Obsidian 为数不多的管理 Obsidian 元数据的，所谓元数据就是指 Obsidian`---` 包裹的前置区域部分，这部分语法使用的是 yaml 格式所以也称为 yaml 区域。

有时候我们的笔记很多元数据都是固定的，虽然通过模板插件 [[math/Config/Template/template-plugin\|template-plugin]] 预设一些固定的 yaml 值，但有时候我们需要一些可选项的值，比如 tags，分类等。这时候 metaedit 就可以提前把可选择项的值维护进去，这样笔记里直接选择就可以了。当然这个插件真正的魅力并不局限于此，它最大的价值就是跟 dataview 联动，弥补 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/dataview\|dataview]] 不能更改查询结果的缺陷。

![metaedit.gif](https://cdn.pkmer.cn/images/202305160840263.gif!pkmer)

## 特性

- 通过命令添加或更新 Yaml 属性和数据视图字段
- 忽略属性以将其从菜单中隐藏
- 可以提前定义属性的值，并给出选择框选择
- 多值模式，允许您根据值检测和矢量化/创建数组
- 进度 自动更新属性/字段的属性
    - 可以统计 checkbox 的总任务数、已完成任务数和未完成任务计数。将任务标记为已完成，文件将使用新计数进行更新。
- 在 YAML 和数据视图之间转换属性
- 轻松删除属性
- 跟看板插件联动，拖动看板会更新对应属性的值
- 通过文件菜单编辑元数据
- 编辑标签中的最后一个值 。
- 提供 API 跟其他插件和模板程序联动。

## 相关设置项

- 进度属性
  ![image.png](https://cdn.pkmer.cn/images/202305160914645.png!pkmer)
如果笔记中有任务勾选，yaml 区域写上 `Total` `Completed` `Incomplete` 字段，会自动更新这些字段对应的值，代表任务总数，已完成任务数，未完成任务数。
![image.png](https://cdn.pkmer.cn/images/202305160921040.png!pkmer)

- 自动属性
  ![image.png](https://cdn.pkmer.cn/images/202305160922182.png!pkmer)

如果 yaml 区域有这些字段，`ctrl+p` → `run metaedit` 选择 `当前进度`，就会给出选择框显示预设的值，跟 dv 联动的时候，主要就是维护这个里面的值。

![image.png](https://cdn.pkmer.cn/images/202305160923380.png!pkmer)

- 忽略属性设置和 yaml 的字段的显示形式设置
![image.png](https://cdn.pkmer.cn/images/202305160926477.png!pkmer)
- 看板助手
  这个就是跟 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-kanban\|obsidian-kanban]] 插件联动
  ![image.png](https://cdn.pkmer.cn/images/202305160928491.png!pkmer)
比如这个看板，我嵌入了一个 `案例进展情况.md` 文件,yaml 区域有个设置中提前设置好的 progress 属性，那么当我把这个文件拖动到 `正在进行` 板块时，`案例进展情况.md` 文件的 progress 的值会自动变成 `正在进行`。

![222.gif](https://cdn.pkmer.cn/images/202305160948232.gif!pkmer)

## 高级用法

跟其他插件联动，用来修改 yaml 数据的值，比如跟 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/dataview\|dataview]] 和 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/buttons\|buttons]]

````
<pre class="dataview dataview-error">Dataview JS queries are disabled. You can enable them in the Dataview settings.</pre>
````

> [!Tip] 推荐阅读
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/frontmatter-alias-display\|frontmatter-alias-display]]：让你的笔记名下直接看到别名
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-metatable\|obsidian-metatable]]：美化 frontmatter 的显示样式
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-view-mode-by-frontmatter\|obsidian-view-mode-by-frontmatter]]：自定义每个笔记的视图
> - [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/obsidian-meta-bind-plugin\|obsidian-meta-bind-plugin]]：让你的笔记具有交互性，通过各种控件修改笔记信息