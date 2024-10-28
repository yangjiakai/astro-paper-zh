---
author: Sat Naing
pubDatetime: 2022-09-26T12:13:24Z
modDatetime: 2024-01-04T09:09:06Z
title: 预定义配色方案
slug: predefined-color-schemes
featured: false
draft: false
tags:
  - color-schemes
description: 为 AstroPaper 博客主题精心制作的一些预定义配色方案。
---

我为这个 AstroPaper 博客主题制作了一些预定义的配色方案。你可以用这些配色方案替换原有的配色。

如果你不知道如何配置配色方案，请查看[这篇博文](https://astro-paper.pages.dev/posts/customizing-astropaper-theme-color-schemes/)。

## 目录

## 浅色配色方案

浅色配色方案必须使用 CSS 选择器 `:root` 和 `html[data-theme="light"]` 来定义。

### 龙虾配色

![龙虾配色方案](https://user-images.githubusercontent.com/53733092/192282447-1d222faf-a3ce-44a9-9cfe-ac873155e5a9.png)

```css
:root,
html[data-theme="light"] {
  --color-fill: 246, 238, 225;
  --color-text-base: 1, 44, 86;
  --color-accent: 225, 74, 57;
  --color-card: 217, 209, 195;
  --color-card-muted: 239, 216, 176;
  --color-border: 220, 152, 145;
}
```

### 叶蓝配色

![叶蓝配色方案](https://user-images.githubusercontent.com/53733092/192318782-e80e3c39-54b5-423e-8f4b-9ae60402fc8d.png)

```css
:root,
html[data-theme="light"] {
  --color-fill: 242, 245, 236;
  --color-text-base: 53, 53, 56;
  --color-accent: 17, 88, 209;
  --color-card: 206, 213, 180;
  --color-card-muted: 187, 199, 137;
  --color-border: 124, 173, 255;
}
```

### 粉红浅色

![粉红配色方案](https://user-images.githubusercontent.com/53733092/192286510-892d0042-2d6d-471e-bb72-954221ae2d17.png)

```css
:root,
html[data-theme="light"] {
  --color-fill: 250, 252, 252;
  --color-text-base: 34, 46, 54;
  --color-accent: 211, 0, 106;
  --color-card: 234, 206, 219;
  --color-card-muted: 241, 186, 212;
  --color-border: 227, 169, 198;
}
```

## 深色配色方案

深色配色方案必须定义为 `html[data-theme="dark"]`。

### AstroPaper 1 原始深色主题

![AstroPaper 1 默认深色主题](https://user-images.githubusercontent.com/53733092/215769153-13b0ad8d-5ba2-44b1-af06-e5ae61293f62.png)

```css
html[data-theme="dark"] {
  --color-fill: 47, 55, 65;
  --color-text-base: 230, 230, 230;
  --color-accent: 26, 217, 217;
  --color-card: 63, 75, 90;
  --color-card-muted: 89, 107, 129;
  --color-border: 59, 70, 85;
}
```

### 深牡蛎配色

![深牡蛎配色方案](https://user-images.githubusercontent.com/53733092/192314524-45ec5904-3d8f-450a-9edf-1e32c5e11d6c.png)

```css
html[data-theme="dark"] {
  --color-fill: 33, 35, 61;
  --color-text-base: 244, 247, 245;
  --color-accent: 255, 82, 86;
  --color-card: 57, 60, 102;
  --color-card-muted: 74, 78, 134;
  --color-border: 177, 47, 50;
}
```

### 粉红深色

![粉红深色配色方案](https://user-images.githubusercontent.com/53733092/192307050-fbd55326-911c-4001-87c6-a8ad9378ac2e.png)

```css
html[data-theme="dark"] {
  --color-fill: 53, 54, 64;
  --color-text-base: 233, 237, 241;
  --color-accent: 255, 120, 200;
  --color-card: 75, 76, 89;
  --color-card-muted: 113, 85, 102;
  --color-border: 134, 67, 107;
}
```

### Astro 深色（高对比度）

![astro-深色配色方案](https://user-images.githubusercontent.com/53733092/215680520-59427bb0-f4cb-48c0-bccc-f182a428d72d.svg)

```css
html[data-theme="dark"] {
  --color-fill: 16, 23, 42; /* 更高对比度背景色 */
  --color-fill: 33, 39, 55;
  --color-text-base: 234, 237, 243;
  --color-accent: 255, 107, 1;
  --color-card: 27, 39, 70;
  --color-card-muted: 138, 51, 2;
  --color-border: 171, 75, 8;
}
```

### Astro 深色（AstroPaper 2 中的新默认深色主题）

![新深色配色方案 - 低对比度](https://user-images.githubusercontent.com/53733092/215772856-d5b7ae35-ddaa-4ed6-b0bf-3fa5dbcf834c.png)

```css
html[data-theme="dark"] {
  --color-fill: 33, 39, 55; /* 较低对比度背景色 */
  --color-text-base: 234, 237, 243;
  --color-accent: 255, 107, 1;
  --color-card: 52, 63, 96;
  --color-card-muted: 138, 51, 2;
  --color-border: 171, 75, 8;
}
```

### Astro 深紫色（AstroPaper 3 中的新深色主题）

![AstroPaper v3 新主题](https://github.com/satnaing/astro-paper/assets/53733092/c8b5d7e1-a3bc-4852-a5ad-4abf7b3cec79)

```css
html[data-theme="dark"] {
  --color-fill: 33, 39, 55;
  --color-text-base: 234, 237, 243;
  --color-accent: 235, 63, 211;
  --color-card: 52, 63, 96;
  --color-card-muted: 125, 79, 124;
  --color-border: 100, 36, 81;
}
```

### AstroPaper v4 特别版（AstroPaper 4 中的新深色主题）

![AstroPaper v4 新主题](https://github.com/satnaing/astro-paper/assets/53733092/66eb74dc-7a0e-4f2e-982d-25f5c443b25a)

```css
html[data-theme="dark"] {
  --color-fill: 0, 1, 35;
  --color-accent: 97, 123, 255;
  --color-text-base: 234, 237, 243;
  --color-card: 33, 34, 83;
  --color-card-muted: 12, 14, 79;
  --color-border: 48, 63, 138;
}
```
