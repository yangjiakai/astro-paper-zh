---
author: Sat Naing
pubDatetime: 2023-09-25T10:25:54.547Z
title: AstroPaper 3.0
slug: astro-paper-v3
featured: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - release
description: "AstroPaper 第3版：借助 Astro v3 和流畅的视图转换提升您的网页体验"
---

我们很高兴地宣布 AstroPaper v3 的发布，这个版本包含了新功能、增强功能和错误修复，以提升您的网页开发体验。让我们来看看这个版本的亮点：

[AstroPaper v3 图片]

## 目录

## 功能和变更

### Astro v3 集成

[视频演示]

AstroPaper 现在完全支持 [Astro v3](https://astro.build/blog/astro-3/)，提供更好的性能和渲染速度。

此外，我们还添加了对 Astro 的 [ViewTransitions API](https://docs.astro.build/en/guides/view-transitions/) 的支持，让您能够创建引人注目和动态的视图转换效果。

在"最近文章"部分，只会显示非精选文章，以避免重复并更好地支持 ViewTransitions API。

### 更新 OG 图片生成逻辑

[示例 OG 图片]

我们更新了自动 OG 图片生成的逻辑，使其更加可靠和高效。此外，它现在支持文章标题中的特殊字符，确保社交媒体预览准确、灵活且吸引眼球。

`SITE.ogImage` 现在是可选的。如果未指定，AstroPaper 将使用 `SITE.title`、`SITE.desc` 和 `SITE.website` 自动生成 OG 图片。

### 主题 meta 标签

添加了主题颜色 meta 标签，可以动态适应主题切换，确保流畅的用户体验。

> 注意顶部的区别

**_AstroPaper v2 主题切换_**

[视频演示]

**_AstroPaper v3 主题切换_**

[视频演示]

## 其他变更

### Astro Prettier 插件

内置安装了 Astro Prettier 插件，以保持项目整洁有序。

### 细微样式变更

解决了单行代码块换行问题，使您的代码片段看起来更加整洁。

更新了导航样式 CSS，允许在导航中添加更多导航链接。

## 升级到 AstroPaper v3

> 本节仅适用于想从旧版本升级到 AstroPaper v3 的用户。

本节将帮助您从 AstroPaper v2 迁移到 AstroPaper v3。

在阅读本节其余部分之前，您可能还想查看[这篇文章](https://astro-paper.pages.dev/posts/how-to-update-dependencies/)，了解如何升级依赖项和 AstroPaper。

## 选项1：全新重启（推荐）

在此版本中，我们进行了大量更改——替换旧的 Astro API 为新 API、修复错误、添加新功能等。因此，如果您没有做太多自定义修改，应该选择这种方法。

**_步骤1：保留所有已更新的文件_**

保留所有已经更新的文件很重要。这些文件包括：

- `/src/config.ts`（v3 中未改动）
- `/src/styles/base.css`（v3 中有少量更改；如下所示）
- `/src/assets/`（v3 中未改动）
- `/public/assets/`（v3 中未改动）
- `/content/blog/`（这是您的博客内容目录 🤷🏻‍♂️）
- 您做的任何其他自定义修改。

```css
/* 文件：/src/styles/base.css */
@layer base {
  /* 其他代码 */
  ::-webkit-scrollbar-thumb:hover {
    @apply bg-skin-card-muted;
  }

  /* 旧代码
  code {
    white-space: pre;
    overflow: scroll;
  } 
  */

  /* 新代码 */
  code,
  blockquote {
    word-wrap: break-word;
  }
  pre > code {
    white-space: pre;
  }
}

@layer components {
  /* 其他代码 */
}
```

**_步骤2：用 AstroPaper v3 替换其他所有内容_**

在此步骤中，除了上述文件/目录（以及您的自定义文件/目录）外，用 AstroPaper v3 替换所有内容。

**_步骤3：模式更新_**

请注意，`/src/content/_schemas.ts` 已被替换为 `/src/content/config.ts`。

此外，`/src/content/config.ts` 不再导出 `BlogFrontmatter` 类型。

因此，文件中所有的 `BlogFrontmatter` 类型需要更新为 `CollectionEntry<"blog">["data"]`。

例如：`src/components/Card.tsx`

```ts
// AstroPaper v2
import type { BlogFrontmatter } from "@content/_schemas";

export interface Props {
  href?: string;
  frontmatter: BlogFrontmatter;
  secHeading?: boolean;
}
```

```ts
// AstroPaper v3
import type { CollectionEntry } from "astro:content";

export interface Props {
  href?: string;
  frontmatter: CollectionEntry<"blog">["data"];
  secHeading?: boolean;
}
```

## 选项2：使用 Git 升级

不推荐大多数用户使用这种方法。如果可以，您应该选择"选项1"。只有在您知道如何解决合并冲突且知道自己在做什么的情况下才使用这种方法。

实际上，我已经为这种情况写了一篇博客文章，您可以在[这里](https://astro-paper.pages.dev/posts/how-to-update-dependencies/#updating-astropaper-using-git)查看。

## 结语

准备好探索 AstroPaper v3 中令人兴奋的新功能和改进了吗？立即开始[使用 AstroPaper](https://github.com/satnaing/astro-paper)。

关于其他错误修复和集成更新，请查看[发布说明](https://github.com/satnaing/astro-paper/releases/tag/v3.0.0)了解更多信息。

如果您在升级过程中遇到任何错误或困难，请随时在 [GitHub](https://github.com/satnaing/astro-paper) 上提出问题或开始讨论。
