---
author: Simon Smale
pubDatetime: 2024-01-08T18:16:00.000Z
modDatetime:
title: 如何在 AstroPaper 中添加新的社交图标
featured: false
draft: false
tags:
  - FAQ
description: 如何在 AstroPaper 中添加新的社交图标
---

新兴平台？互联网的小众角落？或者是你所在地区特有的平台？本文将指导你如何在主题中添加新的社交图标。

## 目录

## 合并回主题

主题的维护者 [Sat Naing](https://github.com/satnaing) 表示他只打算

> 让项目保持支持特定的一些流行社交图标。

所以你的图标可能不会出现在代码库中，但别担心，添加自己的图标非常简单！

## 匹配图标风格

主题使用的图标集来自 [Tabler](https://tabler.io/icons)，那里有相当多的品牌图标。

## 通过示例添加图标

在本指南中，我们将以 StackOverflow 图标为例。

### 查找图标

> 在本例中，我们将使用 `StackOverflow` 作为示例。

在 Tabler 中搜索 'StackOverflow'，我们得到一个图标 <https://tabler.io/icons/icon/brand-stackoverflow>，我们需要它的 svg 代码，先保存下来。

```html
<svg
  xmlns="http://www.w3.org/2000/svg"
  class="icon icon-tabler icon-tabler-brand-stackoverflow"
  width="24"
  height="24"
  viewBox="0 0 24 24"
  stroke-width="2"
  stroke="currentColor"
  fill="none"
  stroke-linecap="round"
  stroke-linejoin="round"
>
  <path stroke="none" d="M0 0h24v24H0z" fill="none" />
  <path d="M4 17v1a2 2 0 0 0 2 2h12a2 2 0 0 0 2 -2v-1" />
  <path d="M8 16h8" />
  <path d="M8.322 12.582l7.956 .836" />
  <path d="M8.787 9.168l7.826 1.664" />
  <path d="M10.096 5.764l7.608 2.472" />
</svg>
```

### 清理代码

我们需要对主题提供的代码进行一些整理。

1. 只保留 `icon-tabler` class
2. 移除 width 和 height
3. 移除 viewBox
4. 移除 stroke-width
5. 移除 stroke
6. 移除 fill

整理后应该如下所示：

```html
<svg
  xmlns="http://www.w3.org/2000/svg"
  class="icon-tabler
  stroke-linecap="round" stroke-linejoin="round"
>
  <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
  <path d="M4 17v1a2 2 0 0 0 2 2h12a2 2 0 0 0 2 -2v-1" />
  <path d="M8 16h8" />
  <path d="M8.322 12.582l7.956 .836" />
  <path d="M8.787 9.168l7.826 1.664" />
  <path d="M10.096 5.764l7.608 2.472" />
</svg>
```

现在我们可以将清理过的 svg 代码添加到 `src/assets/socialIcons.ts` 文件中的 `SocialIcons` 对象中。

```typescript
const socialIcons = {
  /* 其他图标 */
  StackOverflow: `<svg
       xmlns="http://www.w3.org/2000/svg"
       class="icon-tabler
       stroke-linecap="round" stroke-linejoin="round"
     >
       <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
       <path d="M4 17v1a2 2 0 0 0 2 2h12a2 2 0 0 0 2 -2v-1" />
       <path d="M8 16h8" />
       <path d="M8.322 12.582l7.956 .836" />
       <path d="M8.787 9.168l7.826 1.664" />
       <path d="M10.096 5.764l7.608 2.472" />
     </svg>`,
};
```

最后，我们可以在 `src/config.ts` 中的 `SOCIALS` 下配置它。设置 `active: true` 将其添加到网站中。

```typescript
export const SOCIALS: SocialObjects = [
  /* 其他社交平台 */
  {
    name: "StackOverflow",
    href: "https://stackoverflow.com/search?q=astropaper",
    linkTitle: `在 StackOverflow 上查看关于 ${SITE.title} 的问题`,
    active: true,
  },
];
```

> 确保更新 `href` 和 `linkTitle` 为相应的链接和标签。

以上步骤的完整代码可以在[这个 pull request](https://github.com/satnaing/astro-paper/pull/216/files) 中找到。
