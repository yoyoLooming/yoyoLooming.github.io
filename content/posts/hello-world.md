---
title: "你好，世界"
date: 2026-11-12T14:00:00+08:00
draft: true
description: "这是第一篇文章的骨架，填好内容后把 draft 改成 false 就会出现在网站上。"
tags: [随笔]
categories: 随笔
comment: true
---

这里是正文，用 Markdown 写。

## 二级标题

一段普通的话。可以说说今天做了什么、想了什么。

- 列表第一条
- 列表第二条

```python
print("hello world")
```

## 图片

把图片放进 `static/images/` 目录，然后这样引用：

```markdown
![描述](/images/你的图片名.jpg)
```

## 写完要做的三件事

1. 把上面的 `draft: true` 改成 `draft: false`
2. 跑一遍预览看看排版：`hugo server`
3. 提交并推送：

```powershell
git add -A
git commit -m "新增文章：你好，世界"
git push
```
