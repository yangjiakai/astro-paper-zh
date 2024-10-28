---
title: 我是如何开发我的作品集网站和博客的
author: Sat Naing
pubDatetime: 2022-03-25T16:55:12.000+00:00
slug: how-do-i-develop-my-portfolio-and-blog
featured: false
draft: false
tags:
  - NextJS
  - TailwindCSS
  - HeadlessCMS
  - Blog
description: "示例文章：我使用 NextJS 和无头 CMS 开发第一个作品集网站和博客的经历。"
---

> 这篇文章最初发表在我的[博客文章](https://satnaing.dev/blog/posts/how-do-i-develop-my-portfolio-and-blog)中。我放这篇文章是为了展示如何使用 AstroPaper 主题写博客文章。

我使用 NextJS 和无头 CMS 开发第一个作品集网站和博客的经历。

![构建作品集](https://satnaing.dev/_ipx/w_2048,q_75/https%3A%2F%2Fres.cloudinary.com%2Fnoezectz%2Fimage%2Fupload%2Fv1653050141%2FSatNaing%2Fblog_at_cafe_ei1wf4.jpg?url=https%3A%2F%2Fres.cloudinary.com%2Fnoezectz%2Fimage%2Fupload%2Fv1653050141%2FSatNaing%2Fblog_at_cafe_ei1wf4.jpg&w=2048&q=75)

## 动机

从大学时代起，我就一直在想要用自己的域名(**satnaing.dev**)启动一个网站。但直到这个项目之前，这个想法一直没有实现。我做过几个关于 Web 应用开发的项目，但我没有为此付出努力。

那么，"博客呢？"你可能会问。是的，博客也在我的项目清单中有一段时间了。我一直想用一些最新的技术做一个博客项目。然而，我一直忙于工作和其他项目，所以博客项目一直没有开始。

这些天，我倾向于开发注重质量而不是数量的项目。项目完成后，我通常会在 Github 仓库中放一个适当的 readme 文件。但 Github 仓库的 readme 只适合技术方面（这只是我的想法）。我想记录下我的经历和挑战。因此，我决定建立自己的博客。另外，在这一点上，我有足够的经验和信心来开发这个项目。

## 技术栈

对于前端，我想使用 [React](https://reactjs.org/ "React 官方网站")。但仅仅使用 React 对 SEO 来说还不够好；而且我必须考虑很多因素，比如路由、图片优化等。所以，我选择 [NextJS](https://nextjs.org/ "NextJS 官方网站") 作为我的主要前端技术栈。当然还有用于类型检查的 TypeScript。（据说当你习惯了 TypeScript 就会爱上它 😉）

对于样式，我使用 [TailwindCSS](https://tailwindcss.com/ "Tailwind CSS 官方网站")。这是因为我喜欢 Tailwind 提供的开发体验，与其他组件 UI 库（如 MUI 或 React Bootstrap）相比，它有很多灵活性。

这个项目的所有内容都存放在 GitHub 仓库中。我所有的博客文章（包括这一篇）都是用 Markdown 文件格式写的，因为我很习惯这种格式。但为了轻松地编写 Markdown 及其前置元数据，我使用 [Forestry](https://forestry.io/ "Forestry 官方网站") 无头 CMS。它是一个基于 git 的 CMS，可以提供 Markdown 和其他内容。因此，我可以使用 Markdown 或所见即所得编辑器来写内容。此外，用它写前置元数据也很轻松。

图片和资源上传并存储在 [Cloudinary](https://cloudinary.com/ "Cloudinary 官方网站") 中。我通过 Forestry 连接 Cloudinary，并直接在仪表板中管理它们。

总的来说，这些是我为这个项目使用的技术栈：

- 前端：NextJS (TypeScript)
- 样式：TailwindCSS
- 动画：GSAP
- CMS：Forestry 无头 CMS
- 部署：Vercel

## 特性

以下是我的作品集和博客的一些特性

### SEO 友好

整个项目的开发都考虑到了 SEO。我使用了适当的元标签、描述和标题对齐。这个网站现在已被 Google 索引。

> 你可以在 Google 上使用关键词如 'sat naing dev' 搜索这个网站

![在谷歌上搜索 satnaing.dev](https://res.cloudinary.com/noezectz/image/upload/v1648231400/SatNaing/satnaing-on-google_asflq6.png "satnaing.dev 已被索引")

此外，由于正确使用了元标签，这个网站在社交媒体上分享时会显示得很好。

![分享到 Facebook 时的 satnaing.dev 卡片布局](https://res.cloudinary.com/noezectz/image/upload/v1653106955/SatNaing/satnaing-dev-share-on-facebook_1_zjoehx.png "分享到 Facebook 时的卡片布局")

### 动态站点地图

站点地图在 SEO 中扮演着重要角色。因此，这个网站的每个页面都应该包含在 sitemap.xml 中。我在网站中做了一个自动生成的站点地图，每当我创建新的内容、标签或分类时都会更新。

### 明暗主题

由于近年来暗色主题的趋势，现在许多网站都默认包含暗色主题。当然，我的网站也支持明暗主题。

### 完全可访问

这个网站完全可访问。你可以只使用键盘就能导航。我采用了所有的 a11y 增强最佳实践，如在所有图片中包含替代文本、不跳过标题、使用语义化 HTML 标签、正确使用 aria 属性。

### 搜索框、分类和标签

所有博客内容都可以通过搜索框搜索。此外，内容可以通过分类和标签进行筛选。这样，博客读者可以搜索和阅读他们真正想要的内容。

### 性能和 Lighthouse 评分

由于适当的开发和最佳实践，这个网站获得了很好的性能和 Lighthouse 评分。这是这个网站的 Lighthouse 评分。

![satnaing.dev Lighthouse 评分](https://user-images.githubusercontent.com/53733092/159957822-7082e459-11e9-4616-8f1e-49d0881f7cbb.png "satnaing.dev Lighthouse 评分")

### 动画

最初我使用 [Framer Motion](https://www.framer.com/motion/ "Framer Motion") 为这个网站添加动画和微交互。然而，当我尝试使用一些复杂的动画和视差效果时，我发现与 Framer Motion 集成不太方便（可能是因为我不太擅长也不太习惯使用它）。因此，我决定使用 [GSAP](https://greensock.com/ "GSAP 动画库") 来实现所有的动画。它是最流行的动画库之一，能够实现复杂和高级的动画。你可以在这个网站的几乎每个页面上看到动画和微交互。

![satnaing.dev 的动画](https://res.cloudinary.com/noezectz/image/upload/v1653108324/SatNaing/ezgif.com-gif-maker_2_hehtlm.gif "satnaing.dev 网站")

## 结语

总的来说，这个项目让我获得了很多关于开发博客站点（SSG）的经验和信心。现在，我已经掌握了基于 git 的 CMS 的知识，以及它如何与 NextJS 交互。我还学习了 SEO、动态站点地图生成和 Google 索引程序。我将在未来制作更好的项目。敬请期待！✌🏻

最后但同样重要的是，我要感谢我的朋友 [Swann Fevian Kyaw](https://www.facebook.com/bon.zai.3910 "Swann Fevian Kyaw 的 Facebook 账号") (@[ToonHa](https://www.facebook.com/ToonHa-102639465752883 "ToonHa Facebook 页面"))，他为我的网站主页部分画了一个漂亮的插图。

## 项目链接

- 网站：[https://satnaing.dev/](https://satnaing.dev/ "https://satnaing.dev/")
- 博客：[https://satnaing.dev/blog](https://satnaing.dev/blog "https://satnaing.dev/blog")
- 代码仓库：[https://github.com/satnaing/my-portfolio](https://github.com/satnaing/my-portfolio "https://github.com/satnaing/my-portfolio")
