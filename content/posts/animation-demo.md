---
title: "在博客里放一段可交互的动画"
date: 2026-11-13T12:00:00+08:00
draft: true
description: "用 shortcode + iframe 的方式嵌入 canvas 动画，md 只写一行。"
tags: [Hugo, 前端]
categories: 技术
comment: true
---

下面这段是**真的可以交互**的：把鼠标移上去，粒子会被推开；按住会炸开，松手回位。

{{< anim name="spring-particles" height="440" >}}

<!--more-->

## 它是怎么来的

三个文件，各管一件事：

| 文件 | 作用 |
|---|---|
| `static/anim/spring-particles/index.html` | 动画本体，一个自包含的 HTML 文件（canvas + 原生 JS，零依赖） |
| `layouts/shortcodes/anim.html` | 一个 shortcode，把它包成 iframe |
| 这篇文章 | 只写一行 `{{</* anim name="spring-particles" height="440" */>}}` |

### 为什么用 iframe 而不是直接写 `<script>`

1. **不需要开 `unsafe = true`**：shortcode 输出的 HTML 不会被 Markdown 引擎过滤（实测过）
2. **不会和主题打架**：动画自己的 CSS、`requestAnimationFrame`、鼠标事件都关在 iframe 里
3. **可以单独打开分享**：`/anim/spring-particles/` 本身就是个能跑的页面
4. **调试方便**：直接改那个 HTML 文件，刷新就见效，不用碰 Hugo

## 想加新的动画

1. 建目录 `static/anim/你的名字/`，里面放 `index.html`
2. 文章里写 `{{</* anim name="你的名字" height="500" */>}}`

需要第三方库（p5.js、Three.js、GSAP、anime.js、d3.js）时，把库文件下载到 `static/anim/你的名字/` 目录里本地引用，别用 CDN——国内访问 jsdelivr/unpkg 经常卡。

## 性能与可访问性上已经处理的事

- `devicePixelRatio` 缩放：高分屏不糊
- `resize` 防抖重建：窗口变化不卡死
- iframe `loading="lazy"`：文章不滚到这里就不加载
- `prefers-reduced-motion`：系统开了"减少动态效果"就只画一帧静态图
- `pointer` 事件 + `touch-action: none`：手机上也能玩
