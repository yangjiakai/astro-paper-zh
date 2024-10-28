---
author: Sat Naing
pubDatetime: 2022-09-25T15:20:35Z
title: 自定义 AstroPaper 主题配色方案
featured: false
draft: false
tags:
  - color-schemes
  - docs
description: 如何启用/禁用明暗模式，以及自定义 AstroPaper 主题的配色方案。
---

本文将说明如何为网站启用/禁用明暗模式。此外，你还将学习如何自定义整个网站的配色方案。

## 目录

## 启用/禁用明暗模式

AstroPaper 主题默认包含明暗模式。换句话说，将有两种配色方案——一种用于明亮模式，另一种用于暗黑模式。可以在 `src/config.ts` 文件的 SITE 配置对象中禁用此默认行为。

```js
// 文件：src/config.ts
export const SITE = {
  website: "https://astro-paper.pages.dev/",
  author: "Sat Naing",
  desc: "一个简约、响应式且对 SEO 友好的 Astro 博客主题。",
  title: "AstroPaper",
  ogImage: "astropaper-og.jpg",
  lightAndDarkMode: true, // 默认为 true
  postPerPage: 3,
};
```

要禁用`明暗模式`，将 `SITE.lightAndDarkMode` 设置为 `false`。

## 选择主要配色方案

默认情况下，如果我们禁用 `SITE.lightAndDarkMode`，我们将只获得系统的首选配色方案（prefers-color-scheme）。

因此，要选择主要配色方案而不是首选配色方案，我们必须在 `public/toggle-theme.js` 中的 primaryColorScheme 变量中设置配色方案。

```js
/* 文件：public/toggle-theme.js */
const primaryColorScheme = ""; // "light" | "dark"

// 从本地存储获取主题数据
const currentTheme = localStorage.getItem("theme");

// 其他代码等...
```

**primaryColorScheme** 变量可以有两个值：`"light"`、`"dark"`。如果你不想指定主要配色方案，可以保留空字符串（默认）。

- `""` - 系统的首选配色方案。（默认）
- `"light"` - 使用明亮模式作为主要配色方案。
- `"dark"` - 使用暗黑模式作为主要配色方案。

<details><summary>为什么 'primaryColorScheme' 不在 config.ts 中？</summary>

> 为了避免页面重新加载时的颜色闪烁，我们必须在页面加载时尽早放置切换开关的 JavaScript 代码。这解决了闪烁问题，但作为权衡，我们不能再使用 ESM 导入。

[点击这里](https://docs.astro.build/en/reference/directives-reference/#isinline) 了解更多关于 Astro 的 `is:inline` 脚本。

</details>

## 自定义配色方案

AstroPaper 主题的明暗配色方案都可以自定义。你可以在 `src/styles/base.css` 文件中进行此操作。

```css
/* 文件：src/styles/base.css */
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  :root,
  html[data-theme="light"] {
    --color-fill: 251, 254, 251;
    --color-text-base: 40, 39, 40;
    --color-accent: 0, 108, 172;
    --color-card: 230, 230, 230;
    --color-card-muted: 205, 205, 205;
    --color-border: 236, 233, 233;
  }
  html[data-theme="dark"] {
    --color-fill: 47, 55, 65;
    --color-text-base: 230, 230, 230;
    --color-accent: 26, 217, 217;
    --color-card: 63, 75, 90;
    --color-card-muted: 89, 107, 129;
    --color-border: 59, 70, 85;
  }
  /* 其他样式 */
}
```

在 AstroPaper 主题中，`:root` 和 `html[data-theme="light"]` 选择器用作明亮配色方案，`html[data-theme="dark"]` 用作暗黑配色方案。如果你想自定义你的配色方案，你必须在 `:root`、`html[data-theme="light"]` 内指定你的明亮配色方案，在 `html[data-theme="dark"]` 内指定暗黑配色方案。

颜色以 CSS 自定义属性（CSS 变量）表示法声明。颜色属性值以 rgb 值编写。（注意：不要写成 `rgb(40, 39, 40)`，只需指定 `40, 39, 40`）

以下是颜色属性的详细说明。

| 颜色属性             | 定义和用途                                |
| -------------------- | ----------------------------------------- |
| `--color-fill`       | 网站的主要颜色。通常是主背景。            |
| `--color-text-base`  | 网站的次要颜色。通常是文本颜色。          |
| `--color-accent`     | 网站的强调颜色。链接颜色、悬停颜色等。    |
| `--color-card`       | 卡片、滚动条和代码背景颜色（如 `this`）。 |
| `--color-card-muted` | 卡片和滚动条的悬停状态等的背景颜色。      |
| `--color-border`     | 边框颜色。特别用于水平线 (hr)             |

以下是更改明亮配色方案的示例。

```css
@layer base {
  /* 龙虾配色方案 */
  :root,
  html[data-theme="light"] {
    --color-fill: 246, 238, 225;
    --color-text-base: 1, 44, 86;
    --color-accent: 225, 74, 57;
    --color-card: 220, 152, 145;
    --color-card-muted: 233, 119, 106;
    --color-border: 220, 152, 145;
  }
}
```

> 查看一些 AstroPaper 已经为你精心制作的[预定义配色方案](https://astro-paper.pages.dev/posts/predefined-color-schemes/)。
