---
author: Sat Naing
pubDatetime: 2024-01-04T09:30:41.816Z
title: AstroPaper 4.0
slug: "astro-paper-v4"
featured: true
ogImage: ../../assets/images/AstroPaper-v4.png
tags:
  - release
description: "AstroPaper v4: 确保更流畅、功能更丰富的博客体验。"
---

大家好！祝大家新年快乐 🎉，祝愿 2024 年一切顺利！我们很高兴地宣布 AstroPaper v4 的发布，这是一次重要的更新，引入了一系列新功能、改进和错误修复，以提升您的博客体验。非常感谢所有贡献者为实现第 4 版所做的宝贵投入和努力！

[AstroPaper v4 图片]

## 目录

## 重大变更

### 升级到 Astro v4 [#202](https://github.com/satnaing/astro-paper/pull/202)

AstroPaper 现在利用 Astro v4 的功能和能力。不过，这是一个温和的升级，不会影响大多数 Astro 用户。

[Astro v4 图片]

### 用 Astro Content `slug` 替换 `postSlug` [#197](https://github.com/satnaing/astro-paper/pull/197)

博客内容模式中的 `postSlug` 在 AstroPaper v4 中不再可用。最初 Astro 没有 `slug` 机制，因此我们必须自己想办法解决。从 Astro v3 开始，它支持内容集合和 slug 功能。现在，我们认为是时候采用 Astro 的开箱即用 `slug` 功能了。

**_文件: src/content/blog/astro-paper-4.md_**

```bash
---
author: Sat Naing
pubDatetime: 2024-01-01T04:35:33.428Z
title: AstroPaper 4.0
slug: "astro-paper-v4" # 如果未指定 slug，将使用 'astro-paper-4'（文件名）。
# slug: "" ❌ 不能是空字符串
---
```

`slug` 的行为现在略有不同。在 AstroPaper 的早期版本中，如果博客文章（markdown 文件）中未指定 `postSlug`，则该博客文章的标题会被转换为 slug 并用作 `slug`。但在 AstroPaper v4 中，如果未指定 `slug` 字段，将使用 markdown 文件名作为 `slug`。需要注意的是，`slug` 字段可以省略，但不能是空字符串（slug: "" ❌）。

如果您要从 AstroPaper v3 升级到 v4，请确保将 `src/content/blog/*.md` 文件中的 `postSlug` 替换为 `slug`。

## 新功能

### 添加内容创建代码片段 [#206](https://github.com/satnaing/astro-paper/pull/206)

AstroPaper 现在包含用于新博客文章的 VSCode 代码片段，无需手动复制/粘贴 frontmatter 和内容结构（目录、标题、摘要等）。

在[这里](https://code.visualstudio.com/docs/editor/userdefinedsnippets#:~:text=In%20Visual%20Studio%20Code%2C%20snippets,Snippet%20in%20the%20Command%20Palette)了解更多关于 VSCode 代码片段的信息。

[视频演示]

### 在博客文章中添加修改日期时间 [#195](https://github.com/satnaing/astro-paper/pull/195)

通过显示博客文章的修改日期时间，让读者了解最新更新。这不仅增强了用户对文章新鲜度的信任，还有助于提高博客的 SEO。

[最后修改日期功能图片]

如果您对博客文章进行了修改，可以添加 `modDatetime`。现在，文章的排序行为略有不同。所有文章都按 `pubDatetime` 和 `modDatetime` 排序。如果一篇文章同时具有 `pubDatetime` 和 `modDatetime`，其排序位置将由 `modDatetime` 决定。如果没有，则仅考虑 `pubDatetime` 来确定文章的排序顺序。

### 实现返回顶部按钮 [#188](https://github.com/satnaing/astro-paper/pull/188)

通过新实现的返回顶部按钮，增强博客详情文章的用户导航体验。

[返回顶部按钮图片]

### 在标签文章中添加分页 [#201](https://github.com/satnaing/astro-paper/pull/201)

通过在标签文章中添加分页功能，改进内容组织和导航，使用户更容易浏览相关内容。这确保了当一个标签有很多文章时，读者不会被所有相关文章淹没。

[视频演示]

### 动态生成 robots.txt [#130](https://github.com/satnaing/astro-paper/pull/130)

AstroPaper v4 现在可以动态生成 robots.txt 文件，让您更好地控制搜索引擎索引和网络爬虫。此外，sitemap URL 也将添加到 `robot.txt` 文件中。

### 添加 Docker-Compose 文件 [#174](https://github.com/satnaing/astro-paper/pull/174)

通过添加 Docker-Compose 文件，管理 AstroPaper 环境比以往更加容易，简化了部署和配置。

## 重构和错误修复

### 用非 Slugified 标签名替换 Slugified 标题 [#198](https://github.com/satnaing/astro-paper/pull/198)

为了提高清晰度、用户体验和 SEO，标签页面中的标题（`Tag: some-tag`）不再使用 slugified 形式（`Tag: Some Tag`）。

[非 Slugified 标签名图片]

### 实现 100svh 最小高度 ([79d569d](https://github.com/satnaing/astro-paper/commit/79d569d053036f2113519f41b0d257523d035b76))

我们已将 body 的最小高度更新为使用 100svh，为移动用户提供更好的用户体验。

### 更新网站 URL 作为单一事实来源 [#143](https://github.com/satnaing/astro-paper/pull/143)

网站 URL 现在是单一事实来源，简化了配置并避免了不一致性。在这个 [PR](https://github.com/satnaing/astro-paper/pull/143) 及其相关问题中了解更多信息。

### 解决浅色模式下代码块文本不可见的问题 [#163](https://github.com/satnaing/astro-paper/pull/163)

我们修复了浅色模式下代码块文本不可见的问题。

### 在面包屑中解码 Unicode 标签字符 [#175](https://github.com/satnaing/astro-paper/pull/175)

面包屑中的标签最后一部分现在已解码，使非英语 Unicode 字符显示得更好。

### 更新 LOCALE 配置以覆盖整体区域设置 ([cd02b04](https://github.com/satnaing/astro-paper/commit/cd02b047d2b5e3b4a2940c0ff30568cdebcec0b8))

LOCALE 配置已更新，以覆盖更广泛的区域设置，满足更多样化的受众需求。

## 结语

我们相信这些更新将显著提升您的 AstroPaper 体验。感谢每一位贡献者、解决问题的人以及给 AstroPaper 点赞的人。我们期待看到您使用 AstroPaper v4 创作的精彩内容！

博客愉快！

[Sat Naing](https://satnaing.dev) <br/>
AstroPaper 创建者
