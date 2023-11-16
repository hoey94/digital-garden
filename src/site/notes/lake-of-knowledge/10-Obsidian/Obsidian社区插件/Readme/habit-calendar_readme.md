---
{"uid":2023080322192973,"title":"Obsidian 插件：Habit Calendar","tags":["文件管理","任务管理","obsidian插件","readme"],"description":"创建一个可视化的月历视图，让你可以自己添加关键的日期和注意事项。此插件依赖 dataview 插件，并且需要你熟悉 dataviewJS 语法。","author":"AI","type":"readme","draft":false,"editable":false,"modified":20230101000000,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/readme/habit-calendar-readme/","dgPassFrontmatter":true}
---


# Obsidian 插件：Habit Calendar

> [!Note] 插件名片
> - 插件名称：Habit Calendar
> - 插件作者：Hedonihilist
> - 插件说明：创建一个可视化的月历视图，让你可以自己添加关键的日期和注意事项。此插件依赖 dataview 插件，并且需要你熟悉 dataviewJS 语法。
> - 插件分类：[' 文件管理 ', ' 任务管理 ', 'obsidian 插件 ', 'readme']
> - 项目地址：[点我访问](https://github.com/hedonihilist/obsidian-habit-calendar)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?habit-calendar)

## 概述

创建一个可视化的月历视图，让你可以自己添加关键的日期和注意事项。此插件依赖 dataview 插件，并且需要你熟悉 dataviewJS 语法。

![Habit Calendar](https://cdn.pkmer.cn/covers/habit-calendar.GIF!pkmer)

> [!tip] 原文出处
>
>下面自述文件的来源于 [Readme](https://ghproxy.net/https://raw.githubusercontent.com/hedonihilist/obsidian-habit-calendar/master/README.md)
>

---

## Readme(翻译）

下面是 [[habit-calendar\|habit-calendar]] 插件的自述翻译

Obsidian 习惯日历插件

[中文文档](./README-zh.md)

用于 DataviewJS 的月度习惯日历。

该插件可以帮助您在 DataviewJS 代码块中渲染一个日历，显示您在一个月内的习惯状态。它基于 [@duoani](https://github.com/duoani) 的 [Habit Track](https://github.com/duoani/obsidian-habit-tracker) 插件。

该插件旨在与 [DataviewJS](https://blacksmithgu.github.io/obsidian-dataview/) 一起使用。您只需要准备数据并在 dataviewjs 代码块中调用 `renderHabitCalendar` 即可。

有两种方法可以填充日历：

1. Dataview 表格
2. 手动收集的数据

## 更新日志

1.0.x -> 1.1.x

更改了 `renderHabitCalendar` 接口，从

```typescript
renderHabitCalendar(this.container, {
  year: number
  month: number
  width: string
  filepath: string
  format: string
  entries: Entry[]
})
```

到

```typescript
renderHabitCalendar(this.container, dv, {
  year: number  // 必填
  month: number // 必填
  data: any // 必填
  width: string
  format: string
  note_pattern: string
})
```

## 从 Dataview 表格生成日历

为了使其工作，需要准备一个 [Dataview表格](https://blacksmithgu.github.io/obsidian-dataview/queries/query-types/#table)，其中第一列是文件链接，其他列是习惯。

~~~
| File | Coding\|👨‍💻 | Swimming\|🏊 |
| ---- | ------------- | ------------ |

{ .block-language-dataview}
~~~

例如，使用上述 [DQL](https://blacksmithgu.github.io/obsidian-dataview/queries/structure/)，您将获得如下所示的表格：

![dvtable](images/dvtable.png)

要将表格渲染为日历，请将 DQL 的结果传递给 dataviewjs 块中的 `renderHabitCalendar`：

~~~
<pre class="dataview dataview-error">Dataview JS queries are disabled. You can enable them in the Dataview settings.</pre>
~~~

日历应该如下所示：

![calendar](images/hbcalendar.png)

请注意，您可以通过将标题设置为 "aaabbbccc|label" 来自定义日历中的习惯标签👨‍💻。最后一个 "|" 后面的文本将用作标签。

### 不使用 YYYY-MM-DD 格式？

如果您不使用每日笔记的 'YYYY-MM-DD' 命名模式，您可以在调用 `renderHabitCalendar` 时设置模式，以便该插件可以将习惯与正确的每日笔记关联起来：

~~~
<pre class="dataview dataview-error">Dataview JS queries are disabled. You can enable them in the Dataview settings.</pre>
~~~

手动收集数据的日历

该插件还接受自定义数据，请跳转到底部查看详细用法。

### 基本用法

~~~
<pre class="dataview dataview-error">Dataview JS queries are disabled. You can enable them in the Dataview settings.</pre>
~~~

上述代码将呈现如下效果：

![simple](images/simple.png)

如果您的每日笔记采用 `YYYY-MM-DD` 格式，日历将自动与您的每日笔记关联。您可以将鼠标悬停在数字上或单击数字以访问相应的笔记。

![hover](images/hover.gif)

### 使用 HTML 填充日历

想要使用 HTML 填充日历吗？让我们开始吧：

~~~
<pre class="dataview dataview-error">Dataview JS queries are disabled. You can enable them in the Dataview settings.</pre>
~~~

![html](images/html.png)

**注意：** 不要忘记在插件设置中启用 HTML。

### 使用 Markdown 填充日历

如果你不想写 HTML，那就写 Markdown 吧。

~~~
<pre class="dataview dataview-error">Dataview JS queries are disabled. You can enable them in the Dataview settings.</pre>
~~~

![markdown](images/markdown.png)

**注意 1：**有时 Markdown 文本无法正确渲染。尝试切换到其他文件然后再切换回来。

### 自定义链接

如果您希望将习惯与每日笔记关联起来而不是与其他笔记关联，您可以传入每个条目的链接。

假设您希望将第一天链接到一个名为 `Monthly Target.md` 的笔记，将 `link` 属性设置为它：

~~~
<pre class="dataview dataview-error">Dataview JS queries are disabled. You can enable them in the Dataview settings.</pre>
~~~

详细用法

第一个参数应该是将创建日历的 HTML 容器。大多数情况下，使用 `this.container` 即可。

第二个参数应该是 Dataview 对象 `dv`，它将用于获取笔记的信息。

您可以通过第三个参数传递习惯数据。支持以下字段：

- `year`：日历的年份
- `month`：日历的月份
- `data`：该字段可以是 Dataview 表格或包含每天习惯数据的条目列表。一个条目包含：
    - `date`：习惯的日期
    - `content`：您想要放入日历的任何内容
    - `link`：您希望条目链接到的文件，只需传入 `[[]]` 中的文本。例如，如果原始的 Obsidian 链接是 `[[2023-01-01]]`，则传入 `2023-01-01`。
- `format`：您希望如何呈现 `data[i].content`。选择 `html` 或 `markdown` 以呈现为 html 或 markdown，确保在设置选项卡中启用了它们的相应设置。留空将将内容视为纯文本。

如何记录我的习惯

查看 [示例库](https://github.com/hedonihilist/obsidian-habit-calendar/tree/master/ExampleVault)。你的习惯可以看起来像这样

![示例](images/example.png)

### 添加习惯模板

在你的日记模板中，添加一些你想要追踪的习惯：

~~~
```

## 习惯

- [ ] #habit 阅读（reading:: 30）分钟
- [ ] #habit 慢跑（jogging:: 30）分钟
- [ ] #habit 早上8:00之前起床（wakey:: true）
```
~~~

在这里，我们使用 `#habit` 标签来区分习惯和普通任务，并使用 Dataview 属性来记录习惯的强度。

### 记录习惯

完成一个习惯后，在你的日记中勾选相应的习惯。

![勾选习惯](images/check_habits.png)

### 查看你的习惯

使用 dataviewjs 查询已完成的习惯，并将数据传递给 `renderHabitCalendar`。以下代码将查询你进行阅读的天数。

~~~
```
let files = dv.pages(`"diarys"`)
const habit = 'reading'
const year = 2023
const month = 2
const habit_str = '📖 {habit} min'  // {habit}将被替换为相应习惯的值。

let data = []
for (let file of files) {
	console.log(file)
	for (let task of file.file.tasks) {
		if (task.tags.contains('#habit') && task.checked && task[habit]) { // 仅选择已勾选的习惯
			data.push({date: file.file.name, content: habit_str.replace('{habit}', task[habit])})
		}
	} 
}
console.log(data)
renderHabitCalendar(this.container, dv, {year, month, data}) 
```
~~~

![reading](images/reading.png)

### 查看所有习惯

使用以下代码在一个日历中显示所有习惯。

~~~
<pre class="dataview dataview-error">Dataview JS queries are disabled. You can enable them in the Dataview settings.</pre>
~~~

它的显示效果如下图所示：

![all habits](images/allhabits.png)

## 计划

- [x] 点击后直接跳转到日记
- [x] 悬停时预览日记
- [x] 支持在日历中渲染 Markdown



