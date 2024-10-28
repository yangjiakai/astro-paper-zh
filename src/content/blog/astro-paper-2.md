---
author: Sat Naing
pubDatetime: 2023-09-25T10:25:54.547Z
title: AstroPaper 2.0
slug: astro-paper-v2
featured: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - release
description: 基于 Astro v2 增强的 AstroPaper。类型安全的 markdown 内容、bug 修复和更好的开发体验等。
---

Astro 2.0 已经发布,带来了一些很酷的功能、突破性变化、开发体验改进、更好的错误提示等。AstroPaper 利用了这些很酷的功能,特别是 Content Collections API。

[图片: AstroPaper 2.0 介绍]

## 目录

## 功能和变更

### 类型安全的 Frontmatter 和重新定义的博客模式

得益于 Astro 的 Content Collections,AstroPaper 2.0 的 markdown 内容的 frontmatter 现在是类型安全的。博客模式定义在 `src/content/_schemas.ts` 文件中。

### 博客内容的新位置

所有博客文章都从 `src/contents` 移动到了 `src/content/blog` 目录。

### 新的获取 API

现在使用 `getCollection` 函数获取内容。不再需要指定内容的相对路径。

```ts
// 旧的内容获取方法
- const postImportResult = import.meta.glob<MarkdownInstance<Frontmatter>>(
  "../contents/**/**/*.md",);

// 新的内容获取方法
+ const postImportResult = await getCollection("blog");
```

### 改进的搜索逻辑以获得更好的搜索结果

在 AstroPaper 的旧版本中,当有人搜索文章时,会搜索 `title`、`description` 和 `headings`(即博客文章的所有 h1 ~ h6 标题)这些搜索条件键。在 AstroPaper v2 中,用户输入时只会搜索 `title` 和 `description`。

### 重命名的 Frontmatter 属性

以下 frontmatter 属性已重命名:

| 旧名称   | 新名称      |
| -------- | ----------- |
| datetime | pubDatetime |
| slug     | postSlug    |

### 博客文章的默认标签

如果一篇博客文章没有任何标签(换句话说,未指定 frontmatter 属性 `tags`),将使用默认标签 `others`。但你可以在 `/src/content/_schemas.ts` 文件中设置默认标签。

```ts
// src/contents/_schemas.ts
export const blogSchema = z.object({
  // ---
  // 用你想要的任何内容替换 "others"
  tags: z.array(z.string()).default(["others"]),
  ogImage: z.string().optional(),
  description: z.string(),
});
```

### 新的预定义深色配色方案

AstroPaper v2 有一个基于 Astro 深色 logo 的新深色配色方案(高对比度和低对比度)。查看[此链接](https://astro-paper.pages.dev/posts/predefined-color-schemes#astro-dark)了解更多信息。

[图片: 新的预定义深色配色方案]

### 自动类排序

AstroPaper 2.0 包含了使用 [TailwindCSS Prettier 插件](https://tailwindcss.com/blog/automatic-class-sorting-with-prettier)的自动类排序功能。

### 更新的文档和 README

所有[#docs](https://astro-paper.pages.dev/tags/docs/)博客文章和 [README](https://github.com/satnaing/astro-paper#readme)都已针对 AstroPaper v2 进行了更新。

## Bug 修复

- 修复了博客文章页面中的损坏标签
- 在标签页面中,面包屑的最后一部分现在更新为小写以保持一致性
- 在标签页面中排除草稿文章
- 修复页面重新加载后的"onChange 值不更新问题"
