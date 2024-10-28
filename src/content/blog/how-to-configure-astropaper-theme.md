---
author: Sat Naing
pubDatetime: 2022-09-23T04:58:53Z
modDatetime: 2024-10-14T09:27:28.605Z
title: 如何配置 AstroPaper 主题
slug: how-to-configure-astropaper-theme
featured: true
draft: false
tags:
  - configuration
  - docs
description: 如何让 AstroPaper 主题完全符合你的个性化需求。
---

AstroPaper 是一个高度可定制的 Astro 博客主题。使用 AstroPaper，你可以根据个人喜好定制所有内容。本文将介绍如何在配置文件中轻松进行一些自定义设置。

## 目录

## 配置 SITE

重要的配置都在 `src/config.ts` 文件中。在该文件中，你会看到 `SITE` 对象，你可以在其中指定网站的主要配置。

在开发过程中，可以将 `SITE.website` 留空。但在生产模式下，你应该在 `SITE.website` 选项中指定你的部署 URL，因为这将用于规范 URL、社交卡片 URL 等，这些对 SEO 很重要。

```js
// 文件：src/config.ts
export const SITE = {
  website: "https://astro-paper.pages.dev/",
  author: "Sat Naing",
  desc: "一个简约、响应式且对 SEO 友好的 Astro 博客主题。",
  title: "AstroPaper",
  ogImage: "astropaper-og.jpg",
  lightAndDarkMode: true,
  postPerPage: 3,
  scheduledPostMargin: 15 * 60 * 1000, // 15 分钟
  showArchives: true,
  editPost: {
    url: "https://github.com/satnaing/astro-paper/edit/main/src/content/blog",
    text: "建议修改",
    appendFilePath: true,
  },
};
```

以下是 SITE 配置选项：

| 选项                  | 描述                                                                                                                                                                                                                  |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `website`             | 你的网站部署地址                                                                                                                                                                                                      |
| `author`              | 你的名字                                                                                                                                                                                                              |
| `desc`                | 你的网站描述。对 SEO 和社交媒体分享有用。                                                                                                                                                                             |
| `title`               | 你的网站名称                                                                                                                                                                                                          |
| `ogImage`             | 网站的默认 OG 图片。用于社交媒体分享。OG 图片可以是外部图片 URL 或放在 `/public` 目录下。                                                                                                                             |
| `lightAndDarkMode`    | 启用或禁用网站的`明暗模式`。如果禁用，将使用主要配色方案。此选项默认启用。                                                                                                                                            |
| `postPerIndex`        | 在首页`最近`部分显示的文章数量。                                                                                                                                                                                      |
| `postPerPage`         | 你可以指定每个文章页面显示多少篇文章。(例如：如果你将 SITE.postPerPage 设置为 3，每页将只显示 3 篇文章)                                                                                                               |
| `scheduledPostMargin` | 在生产模式下，未来 `pubDatetime` 的文章将不可见。但是，如果文章的 `pubDatetime` 在接下来的 15 分钟内，它将可见。如果你不喜欢默认的 15 分钟间隔，可以设置 `scheduledPostMargin`。                                      |
| `showArchives`        | 确定是否在网站上显示`归档`菜单（位于`关于`和`搜索`菜单之间）及其对应页面。此选项默认设置为 `true`。                                                                                                                   |
| `editPost`            | 此选项允许用户通过在博客文章标题下提供编辑链接来建议更改。可以通过从 `SITE` 配置中删除此功能来禁用它。你还可以将 `appendFilePath` 设置为 `true`，自动将文章的文件路径附加到 URL，将用户引导到他们想要编辑的特定文章。 |

## 配置语言环境

你可以配置用于构建的默认语言环境（例如，文章页面中的日期格式），以及在浏览器中渲染的语言环境（例如，搜索页面中的日期格式）

```js
// 文件：src/config.ts
export const LOCALE = {
  lang: "en", // html 语言代码。设置为空时默认为 "en"
  langTag: ["en-EN"], // BCP 47 语言标签。设置为空 [] 以使用环境默认值
} as const;
```

`LOCALE.lang` 将用作 HTML ISO 语言代码，如 `<html lang="en">`。如果不指定，默认将设置为 `en`。
`LOCALE.langTag` 用作 [datetime locale](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleDateString#locales)。对于这个，你可以指定一个备用语言数组。将 `LOCALE.langTag` 留空 `[]` 以在构建时和运行时使用环境默认值。

## 配置 logo 或标题

你可以在 `src/config.ts` 文件中指定网站的标题或 logo 图片。

![指向网站 logo 的箭头](https://res.cloudinary.com/noezectz/v1663911318/astro-paper/AstroPaper-logo-config_goff5l.png)

```js
// 文件：src/config.ts
export const LOGO_IMAGE = {
  enable: false,
  svg: true,
  width: 216,
  height: 46,
};
```

如果你将 `LOGO_IMAGE.enable` 设置为 `false`，AstroPaper 将自动将 `SITE.title` 转换为主站点文本 logo。

如果你将 `LOGO_IMAGE.enable` 设置为 `true`，AstroPaper 将使用 logo 图片作为网站的主要 logo。

你必须在 `/public/assets` 目录下指定 `logo.png` 或 `logo.svg`。目前仅支持 svg 和 png 图片文件格式。(**_重要！_** _logo 名称必须是 logo.png 或 logo.svg)_

如果你的 logo 图片是 png 文件格式，你必须将 `LOGO_IMAGE.svg` 设置为 `false`。

建议你指定 logo 图片的宽度和高度。你可以通过设置 `LOGO_IMAGE.width` _和_ `LOGO_IMAGE.height` 来实现。

## 配置社交链接

你可以配置自己的社交链接及其图标。

![指向社交链接图标的箭头](https://res.cloudinary.com/noezectz/v1663914759/astro-paper/astro-paper-socials_tkcjgq.png)

目前支持 20 个社交图标。（Github、LinkedIn、Facebook 等）

你可以在主页部分和页脚中指定和启用特定的社交链接。要做到这一点，请转到 `/src/config.ts`，然后你会找到 `SOCIALS` 对象数组。

```js
// 文件：src/config.ts
export const SOCIALS: SocialObjects = [
  {
    name: "Github",
    href: "https://github.com/satnaing/astro-paper",
    linkTitle: ` ${SITE.title} on Github`,
    active: true,
  },
  {
    name: "Facebook",
    href: "https://github.com/satnaing/astro-paper",
    linkTitle: `${SITE.title} on Facebook`,
    active: true,
  },
  {
    name: "Instagram",
    href: "https://github.com/satnaing/astro-paper",
    linkTitle: `${SITE.title} on Instagram`,
    active: true,
  },
  ...
]
```

你必须将特定社交链接设置为 `active: true`，才能在主页和页脚部分显示你的社交链接。然后，你还必须在 `href` 属性中指定你的社交链接。

例如，如果我想让我的 Github 显示出来，我会这样设置：

```js
export const SOCIALS: SocialObjects = [
  {
    name: "Github",
    href: "https://github.com/satnaing", // 更新账号链接
    linkTitle: `${SITE.title} on Github`, // 此文本将在悬停和 VoiceOver 时显示
    active: true, // 确保将 active 设置为 true
  }
  ...
]
```

另一个需要注意的是，你可以在对象中指定 `linkTitle`。这个文本会在鼠标悬停在社交图标链接上时显示。此外，这将改善可访问性和 SEO。AstroPaper 提供默认的链接标题值；但你可以用自己的文本替换它们。

例如，从：

```js
linkTitle: `${SITE.title} on Twitter`,
```

改为：

```js
linkTitle: `Follow ${SITE.title} on Twitter`;
```

## 结论

这是关于如何自定义这个主题的简要说明。如果你懂一些编程，你可以进行更多自定义。关于自定义样式，请阅读[这篇文章](https://astro-paper.pages.dev/posts/customizing-astropaper-theme-color-schemes/)。感谢阅读。✌🏻
