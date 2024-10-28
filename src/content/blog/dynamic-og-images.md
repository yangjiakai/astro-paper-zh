---
author: Sat Naing
pubDatetime: 2022-12-28T04:59:04.866Z
title: AstroPaper 博客文章中的动态 OG 图片生成
slug: dynamic-og-image-generation-in-astropaper-blog-posts
featured: false
draft: false
tags:
  - docs
  - release
description: AstroPaper v1.4.0 的新功能，为博客文章引入动态 OG 图片生成。
---

AstroPaper v1.4.0 的新功能，为博客文章引入动态 OG 图片生成。

## 目录

## 简介

OG 图片（又称社交媒体图片）在社交媒体互动中扮演着重要角色。如果你不知道什么是 OG 图片，它是当我们在 Facebook、Discord 等社交媒体上分享网站 URL 时显示的图片。

> 严格来说，Twitter 使用的社交图片并不叫 OG 图片。但在本文中，我会用 OG 图片这个术语来表示所有类型的社交媒体图片。

## 默认/静态 OG 图片（旧方式）

AstroPaper 已经提供了一种为博客文章添加 OG 图片的方法。作者可以在 frontmatter 的 `ogImage` 中指定 OG 图片。即使作者没有在 frontmatter 中定义 OG 图片，也会使用默认的 OG 图片作为后备方案（在这种情况下是 `public/astropaper-og.jpg`）。但问题是默认的 OG 图片是静态的，这意味着每个没有在 frontmatter 中包含 OG 图片的博客文章都会使用相同的默认 OG 图片，尽管每篇文章的标题/内容都不相同。

## 动态 OG 图片

为每篇文章生成动态 OG 图片使作者可以避免为每篇博客文章指定 OG 图片。此外，这将防止所有博客文章使用相同的后备 OG 图片。

在 AstroPaper v1.4.0 中，使用了 Vercel 的 [Satori](https://github.com/vercel/satori) 包来生成动态 OG 图片。

动态 OG 图片将在构建时为以下博客文章生成：

- 在 frontmatter 中没有包含 OG 图片
- 没有被标记为草稿

## AstroPaper 动态 OG 图片的组成

AstroPaper 的动态 OG 图片包括*博客文章标题*、*作者名称*和*网站标题*。作者名称和网站标题将通过 **"src/config.ts"** 文件中的 `SITE.author` 和 `SITE.title` 获取。标题从博客文章 frontmatter 的 `title` 生成。  
![动态 OG 图片示例链接](https://user-images.githubusercontent.com/53733092/209704501-e9c2236a-3f4d-4c67-bab3-025aebd63382.png)

### 非拉丁字符问题

包含非拉丁字符的标题无法直接正常显示。要解决这个问题，我们需要在 `loadGoogleFont.ts` 中用你偏好的字体替换 `fontsConfig`。

```ts
// 文件：loadGoogleFont.ts

async function loadGoogleFonts(
  text: string
): Promise<
  Array<{ name: string; data: ArrayBuffer; weight: number; style: string }>
> {
  const fontsConfig = [
    {
      name: "Noto Sans JP",
      font: "Noto+Sans+JP",
      weight: 400,
      style: "normal",
    },
    {
      name: "Noto Sans JP",
      font: "Noto+Sans+JP:wght@700",
      weight: 700,
      style: "normal",
    },
    { name: "Noto Sans", font: "Noto+Sans", weight: 400, style: "normal" },
    {
      name: "Noto Sans",
      font: "Noto+Sans:wght@700",
      weight: 700,
      style: "normal",
    },
  ];
  // 其他代码
}
```

> 查看[这个 PR](https://github.com/satnaing/astro-paper/pull/318)获取更多信息。

## 限制

在写这篇文章时，[Satori](https://github.com/vercel/satori) 还相当新，尚未达到主要版本。因此，这个动态 OG 图片功能仍有一些限制。

- 此外，还不支持 RTL 语言。
- 在标题中[使用表情符号](https://github.com/vercel/satori#emojis)可能有点棘手。
