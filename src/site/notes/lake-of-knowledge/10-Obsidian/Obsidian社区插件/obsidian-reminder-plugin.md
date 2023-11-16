---
{"uid":20230329145838,"title":"Obsidian 插件：Reminder 为待办任务增加提醒","tags":["Obsidian","插件","任务提醒"],"description":"Obsidian 插件：Reminder 为待办任务增加提醒","author":"OS","type":"other","draft":false,"editable":false,"modified":20230604174442,"dg-publish":true,"permalink":"/lake-of-knowledge/10-obsidian/obsidian/obsidian-reminder-plugin/","dgPassFrontmatter":true}
---


# Obsidian 插件：Reminder 为待办任务增加提醒

## 概述

该插件可以为你的任务增加提醒，并且可以联动的系统，在系统通知区域显示待办提醒。

> [!Note] 插件名片
> - 插件名称：Reminder
> - 插件作者：uphy
> - 插件说明：为 Markdown 中的待办事项，添加提醒管理。
> - 插件项目地址：[点我跳转](https://github.com/uphy/obsidian-reminder)
> - 国内下载地址：[下载安装](https://pkmer.cn/products/plugin/pluginMarket/?obsidian-reminder-plugin)

## 效果&特性

- 侧边栏 Reminder 面板显示待办事项到期信息
- 点击 Reminder 面板开启该事项所在之笔记

## 安装

1. 进入 Obsidian 社区插件
2. 搜索
3. 安装
4. 开启插件

## 设置

- Reminder Time：预设的到期时间
- Primary reminder format：若需要到期时间则建议选用 Reminder
- 在待办事项后面输入（@日期时间）
- 默认的触发关键字是「（@」，如果 @ 被占用，你也可以使用其他触发关键字

## 使用方法

### 输入方法

- 触发关键字，输入后会弹出日历视窗
- 如果熟悉，也有可以直接 ` (@2021-08-14)` 或 `(@2021-08-14 09:37)`
- Reminder 支持具体到具体的时间点

```语法
- [ ] This is a sample task with reminder (@2021-08-14)
- [ ] Also you can specify time (@2021-08-14 09:37)
- [x] You will not be notified about the reminders you have already checked. (@2021-08-14)
```

![input-reminder-time.gif](https://cdn.pkmer.cn/images/133e1677ca90a3f85d2c38dd280a78d1_MD5.gif!pkmer)

### 查看方法—提醒列表

你可以通过 Reminder 插件自带的面板，查看所有文件中包含的提醒。

如果单击提醒列表项，将跳转显示到对应笔记文件。

![image.png](https://cdn.pkmer.cn/images/5d718b10d449075829627802767c6fed_MD5.png!pkmer)

### 系统通知提醒

![image.png](https://cdn.pkmer.cn/images/67d54efdb120312443fab1bf1b88265a_MD5.png!pkmer)

如果单击 `Mark as Done`（已完成），你的待办项目将被自动标记。另外，您可以通过以后选择 `Remind Me Later`（稍后提醒我），你的提醒将被推迟。

![image.png](https://cdn.pkmer.cn/images/49727fba6c33b84c48cea8c340b9528f_MD5.png!pkmer)

## 与其他插件的兼容性

除原始格式 @yyyy-mm-dd 外，该插件还支持以下插件格式。

- Obsidian Tasks 插件： (e.g. `📅 2021-05-02`)
- Kanban 插件：(e.g. `@{YYYY-MM-DD}`)