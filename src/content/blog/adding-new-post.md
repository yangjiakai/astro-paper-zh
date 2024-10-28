---
author: Sat Naing
pubDatetime: 2022-09-23T15:22:00Z
modDatetime: 2023-12-21T09:12:47.400Z
title: 在 AstroPaper 主题中添加新文章
slug: adding-new-posts-in-astropaper-theme
featured: true
draft: false
tags:
  - docs
description: 使用 AstroPaper 主题创建或添加新文章的一些规则和建议。
---

以下是在 AstroPaper 博客主题中创建新文章的一些规则/建议、提示和技巧。

## 目录

## Frontmatter（前置元数据）

Frontmatter 是存储博客文章（文章）重要信息的主要位置。Frontmatter 位于文章的顶部，使用 YAML 格式编写。在 [astro 文档](https://docs.astro.build/en/guides/markdown-content/) 中了解更多关于 frontmatter 及其用法的信息。

以下是每篇文章的 frontmatter 属性列表。

| 属性               | 描述                                                          | 备注                                       |
| ------------------ | ------------------------------------------------------------- | ------------------------------------------ |
| **_title_**        | 文章标题 (h1)                                                 | 必需<sup>\*</sup>                          |
| **_description_**  | 文章描述。用于文章摘要和网站描述。                            | 必需<sup>\*</sup>                          |
| **_pubDatetime_**  | ISO 8601 格式的发布日期时间。                                 | 必需<sup>\*</sup>                          |
| **_modDatetime_**  | ISO 8601 格式的修改日期时间。(仅在博客文章被修改时添加此属性) | 可选                                       |
| **_author_**       | 文章作者。                                                    | 默认 = SITE.author                         |
| **_slug_**         | 文章的 slug。此字段是可选的，但不能为空字符串。(slug: ""❌)   | 默认 = 文件名转换的 slug                   |
| **_featured_**     | 是否在首页的特色部分显示此文章                                | 默认 = false                               |
| **_draft_**        | 将此文章标记为"未发布"。                                      | 默认 = false                               |
| **_tags_**         | 此文章的相关关键词。以 yaml 数组格式编写。                    | 默认 = others                              |
| **_ogImage_**      | 文章的 OG 图片。用于社交媒体分享和 SEO。                      | 默认 = SITE.ogImage 或生成的 OG 图片       |
| **_canonicalURL_** | 规范 URL（绝对路径），用于文章已存在于其他来源的情况。        | 默认 = `Astro.site` + `Astro.url.pathname` |

> 提示！你可以通过在控制台运行 `new Date().toISOString()` 来获取 ISO 8601 日期时间。记得删除引号。

frontmatter 中只有 `title`、`description` 和 `pubDatetime` 字段是必须指定的。

标题和描述（摘要）对搜索引擎优化（SEO）很重要，因此 AstroPaper 建议在博客文章中包含这些内容。

`slug` 是 URL 的唯一标识符。因此，`slug` 必须是唯一的，与其他文章不同。`slug` 的空格应该用 `-` 或 `_` 分隔，但推荐使用 `-`。Slug 是使用博客文章文件名自动生成的。但是，你可以在博客文章的 frontmatter 中定义你的 `slug`。

例如，如果博客文件名是 `adding-new-post.md` 并且你没有在 frontmatter 中指定 slug，Astro 将使用文件名自动为博客文章创建一个 slug。因此，slug 将是 `adding-new-post`。但如果你在 frontmatter 中指定了 `slug`，这将覆盖默认的 slug。你可以在 [Astro 文档](https://docs.astro.build/en/guides/content-collections/#defining-custom-slugs) 中了解更多相关信息。

如果你在博客文章中省略 `tags`（换句话说，如果没有指定标签），默认标签 `others` 将用作该文章的标签。你可以在 `/src/content/config.ts` 文件中设置默认标签。

```ts
// src/content/config.ts
export const blogSchema = z.object({
  // ---
  draft: z.boolean().optional(),
  tags: z.array(z.string()).default(["others"]), // 用你想要的任何内容替换 "others"
  // ---
});
```

### Frontmatter 示例

以下是文章的 frontmatter 示例。

```yaml
# src/content/blog/sample-post.md
---
title: 文章的标题
author: 你的名字
pubDatetime: 2022-09-21T05:17:19Z
slug: the-title-of-the-post
featured: true
draft: false
tags:
  - some
  - example
  - tags
ogImage: ""
description: 这是示例文章的示例描述。
canonicalURL: https://example.org/my-article-was-already-posted-here
---
```

## 添加目录

默认情况下，文章（文章）不包含任何目录（toc）。要包含目录，你必须以特定方式指定它。

以 h2 格式（markdown 中的 ##）写入 `Table of contents`，并将其放置在你希望它出现在文章中的位置。

例如，如果你想将目录放在介绍段落下方（就像我通常做的那样），你可以通过以下方式实现：

```md
---
# some frontmatter
---

以下是在 AstroPaper 博客主题中创建新文章的一些建议、提示和技巧。

## Table of contents

<!-- 文章的其余部分 -->
```

## 标题

关于标题有一点需要注意。AstroPaper 博客文章使用标题（frontmatter 中的标题）作为文章的主标题。因此，文章中的其余标题应该使用 h2 \~ h6。

这个规则不是强制性的，但为了视觉效果、可访问性和 SEO 目的，强烈建议遵循。

## 存储博客内容的图片

以下是在 markdown 文件中存储和显示图片的两种方法。

> 注意！如果需要在 markdown 中设置优化图片的样式，你应该 [使用 MDX](https://docs.astro.build/en/guides/images/#images-in-mdx-files)。

### 在 `src/assets/` 目录中（推荐）

你可以在 `src/assets/` 目录中存储图片。这些图片将通过 [Image Service API](https://docs.astro.build/en/reference/image-service-reference/) 被 Astro 自动优化。

你可以使用相对路径或别名路径（`@assets/`）来提供这些图片。

示例：假设你想显示路径为 `/src/assets/images/example.jpg` 的 `example.jpg`。

```md
![something](@assets/images/example.jpg)

<!-- 或者 -->

![something](../../assets/images/example.jpg)

<!-- 使用 img 标签或 Image 组件将不起作用 ❌ -->
<img src="@assets/images/example.jpg" alt="something">
<!-- ^^ 这是错误的 -->
```

> 从技术上讲，你可以在 `src` 下的任何目录中存储图片。这里的 `src/assets` 只是一个建议。

### 在 `public` 目录中

你可以在 `public` 目录中存储图片。请记住，存储在 `public` 目录中的图片不会被 Astro 处理，这意味着它们将保持未优化状态，你需要自己处理图片优化。

对于这些图片，你应该使用绝对路径；这些图片可以使用 [markdown 注释](https://www.markdownguide.org/basic-syntax/#images-1) 或 [HTML img 标签](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img) 显示。

示例：假设 `example.jpg` 位于 `/public/assets/images/example.jpg`。

```md
![something](/assets/images/example.jpg)

<!-- 或者 -->

<img src="/assets/images/example.jpg" alt="something">
```

## 附加内容

### 图片压缩

当你在博客文章中放置图片时（特别是 `public` 目录下的图片），建议对图片进行压缩。这将影响网站的整体性能。

我推荐的图片压缩网站：

- [TinyPng](https://tinypng.com/)
- [TinyJPG](https://tinyjpg.com/)

### OG 图片

如果文章没有指定 OG 图片，将使用默认的 OG 图片。虽然不是必需的，但应该在 frontmatter 中指定与文章相关的 OG 图片。OG 图片的推荐尺寸是 **_1200 X 640_** px。

> 从 AstroPaper v1.4.0 开始，如果未指定，OG 图片将自动生成。查看 [公告](https://astro-paper.pages.dev/posts/dynamic-og-image-generation-in-astropaper-blog-posts/)。
