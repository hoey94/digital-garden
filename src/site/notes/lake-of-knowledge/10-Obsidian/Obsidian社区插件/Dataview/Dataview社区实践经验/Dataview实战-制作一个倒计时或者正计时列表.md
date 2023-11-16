---
{"uid":20230915135155,"title":"Dataview 实战：制作一个倒计时或者正计时列表","tags":["Obsidian","dataview","InlineQuery"],"description":"用 Dataview 制作一个倒计时或者正计时列表，展示了今天、本周、本月和今年的剩余时间和已经过去的时间跨度以及百分比。文中给出了代码的具体解释，以及你想定制相对某个特定时间点时修改的方法。","author":"Huajin","type":"other","draft":false,"editable":false,"modified":20230918130039,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/dataview/dataview/dataview/","dgPassFrontmatter":true}
---


# Dataview 实战：制作一个倒计时或者正计时列表

Dataview 是你进阶使用 Obsidian 中不可缺少的一步，通常我们会用 Dataview 来统计收集你的库中满足特定条件的所有笔记。但是你有没有想过，DQL 提供了很多关于时间的 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/15 - Literals 字面常量\|字面量]]，我们完全可以用他们来记录时间。

![Pasted image 20230915140109.png](https://cdn.pkmer.cn/images/Pasted%20image%2020230915140109.png!pkmer)

上面这些，通通是用的 Dataview 的行内查询 (Inline DQL) 实现的，所有的时间记录都会自动修改，不需要手动修改。

> [!warning] 注意
> 使用行内查询之前，需要在 Dataview 设置中打开 Enable Inline Queries 设置。你可以在 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview基本语法/20 - 四种查询方式\|Dataview 的四种查询方式]] 中查看行内查询的简单介绍和语法，可以在 [[lake-of-knowledge/10-Obsidian/Obsidian社区插件/Dataview/Dataview语法实战/Dataview语法实战-行内DQL示例\|Dataview语法实战-行内DQL示例]] 中参看我们提供的一些简单的使用方向。

## 源码

上面图片中使用的源码如下，你可以直接复制全部放到你的首页，也可以只复制其中你需要的某些部分。

```
### 倒计时
- 今天还剩 6.52 小时，也就是 391 分钟，或者是 23470 秒；
- 这周还剩 3.27 天，也就是 78.52 小时，或者是 4711.16 分钟，这一共是 282670 秒；
- 11 月还剩 14.27 天，也就是 342.52 小时，或者是 20551.16 分钟，这一共是 1233070 秒；

*百分比时间*
- 今日剩余：27.16%；
- 本周剩余：46.74%；
- 本月剩余：44.6%；
- 今年剩余：12.4%；

### 正计时
- 今天已经过了 17.48 小时，也就是 1049 分钟，或者是 62930 秒；
- 这周已经过了 89.48 小时，也就是 5369 分钟，或者是 322130 秒；
- 这个月已经过了 377.48 小时，也就是 22649 分钟，或者是 1358930 秒；
- 今年已经过了 7577.48 小时，也就是 454649 分钟，或者是 27278930 秒；

*百分比时间*
- 今日已经过了：72.84%；
- 本周已经过去：53.26%；
- 本月已经过了：49.15%；
- 今年已经过了：86.5%；
```

## 代码解释

- Dataview 为我们提供了许多时间节点的字面量：
	- 某个时间节点的字面量：
		- date(today)：今天的 00:00；
		- date(now)：现在的具体日期加时间；
		- date(tomorrow)：明天的 00:00；
		- date(sow)、date(eow)：这周的开始和结束，sow 是 start of week 的缩写，eow 是 end of week 的缩写；
		- date(som)、date(eom)：这个月的开始和结束，som 是 start of month 的缩写，eom 是 end of month 的缩写；
		- date(som)、date(eom)：这个月的开始和结束，som 是 start of month 的缩写，eom 是 end of month 的缩写；
	- 定长时间的字面量：
		- dur(24 hours)：24 小时的时长；
		- dur(365 d)：365 天；
	- 利用点运算符进行时间转换：
		- date(now).seconds：获得 now 的秒数；
		- date(now).minutes：获得 now 的分数；
		- date(now).hours：获得 now 的小时数；
		- (dur(now) - dur(today)).seconds：获得今天 00:00 到现在所过的时间，并且转化为秒；
		- (dur(now) - dur(today)).minutes：获得今天 00:00 到现在所过的时间，并且转化为分钟；
		- (dur(now) - dur(today)).hours：获得今天 00:00 到现在所过的时间，并且转化为小时；
- 利用 Dataview 提供的四舍五入的 [[25 - Function 函数\|函数]] round() 令结果只显示需要的位数
	- round(number, \[digits])：number 就是四舍五入的数字，digits 就是舍入的位数，可以不填。例如 `round(4.555) = 5`，`round(4.555, 2) = 4.56`。

利用上面的这些简单的部分进行组合，就可以获得剩余时间或者已经过了的时间。当然，我们也不一定非要用 Dataview 提供的这些时间字面量，我们可以用已经确定的时间节点。

用 `date(yyyy-MM-dd)` 的格式可以确定某一个时间点，利用这个时间点再做一些运算，就可以得到一个朋友的生日倒计时的列表、许多节日倒计时的列表等等。