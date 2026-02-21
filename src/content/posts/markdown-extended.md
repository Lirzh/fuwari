---
title: Markdown 扩展功能
published: 2024-05-01
updated: 2024-11-29
description: '了解更多 Fuwari 中的 Markdown 功能'
image: ''
tags: [example]
category: example
draft: true
---

## GitHub 仓库卡片

您可以添加链接到 GitHub 仓库的动态卡片，页面加载时，仓库信息将从 GitHub API 获取。

::github{repo="Fabrizz/MMM-OnSpotify"}

使用代码 `::github{repo="<owner>/<repo>"}` 创建 GitHub 仓库卡片。

```markdown
::github{repo="saicaca/fuwari"}
```

## 提示框

支持以下类型的提示框：`note` `tip` `important` `warning` `caution`

:::note
突出显示用户即使快速浏览也应考虑的信息。
:::

:::tip
可选信息，帮助用户更成功地完成任务。
:::

:::important
用户成功所需的关键信息。
:::

:::warning
由于潜在风险，需要用户立即关注的关键内容。
:::

:::caution
操作的潜在负面后果。
:::

### 基本语法

```markdown
:::note
突出显示用户即使快速浏览也应考虑的信息。
:::

:::tip
可选信息，帮助用户更成功地完成任务。
:::
```

### 自定义标题

提示框的标题可以自定义。

:::note[我的自定义标题]
这是一个带有自定义标题的提示框。
:::

```markdown
:::note[我的自定义标题]
这是一个带有自定义标题的提示框。
:::
```

### GitHub 语法

> [!TIP]
> [GitHub 语法](https://github.com/orgs/community/discussions/16925)也被支持。

```
> [!NOTE]
> GitHub 语法也被支持。

> [!TIP]
> GitHub 语法也被支持。
```

### 隐藏内容

您可以在文本中添加隐藏内容。文本也支持 **Markdown** 语法。

内容 :spoiler[被隐藏了 **嘿嘿**]！

```markdown
内容 :spoiler[被隐藏了 **嘿嘿**]！