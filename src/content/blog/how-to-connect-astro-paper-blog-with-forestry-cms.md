---
title: 如何将 AstroPaper 博客与 Forestry CMS 连接
author: Sat Naing
pubDatetime: 2022-09-21T05:17:19Z
slug: how-to-connect-astro-paper-blog-with-forestry-cms
featured: false
draft: false
tags:
  - docs
  - forestry-cms
  - astro-paper
ogImage: https://res.cloudinary.com/noezectz/v1663745737/astro-paper/astropaper-x-forestry-og_kqfwp0.png
description: 将 Astro-Paper 博客主题与 Forestry Headless CMS 连接的步骤详解。
---

> 重要提示!!! Forestry 将于2023年4月22日停止服务。你可以[阅读他们的公告](https://forestry.io/blog/forestry.io-end-of-life/)了解更多信息。

在本文中，我将详细解释如何将 AstroPaper 主题与 Forestry headless CMS 连接的步骤。让我们开始吧 🎉

## 目录

## 什么是 Forestry？

[Forestry](https://forestry.io/ "Forestry 网站")是一个基于 git 的 headless CMS，我们可以通过它轻松管理我们的 markdown 内容。虽然它不是开源的 CMS，但它有一个不错的免费计划，可以导入最多3个站点（3个代码仓库）。在本文中，我将演示如何将 Forestry 作为我们 AstroPaper 博客主题的基于 git 的 CMS。

## 在 Forestry.io 登录/注册账号

首先，你需要在 [Forestry 网站](https://app.forestry.io/login "Forestry 登录页面")创建一个账号。我通常使用 Github 账号登录。

![Forestry 登录页面](https://res.cloudinary.com/noezectz/v1663739096/astro-paper/Forestry-io_hk5yzv.png)

## 导入 AstroPaper 站点（代码仓库）

这部分是将代码仓库导入到 Forestry 并进行一些基础设置。

### 添加站点

登录/注册账号后，点击"Add Site"按钮导入你的 AstroPaper 站点。

![Forestry '我的站点'页面](https://res.cloudinary.com/noezectz/v1663739752/astro-paper/Forestry-io_1_z1bdyd.png)

### 选择静态站点生成器

在这种情况下，只需选择"Others"

![选择'Others'作为站点生成器](https://res.cloudinary.com/noezectz/v1663740872/astro-paper/Forestry-io_2_blrrw2.png)

### 选择 Git 提供商

我的 git 提供商是 Github，我假设你的也是一样。所以，选择"Github"。

![选择 Github 作为 git 提供商](https://res.cloudinary.com/noezectz/v1663740922/astro-paper/Forestry-io_3_pj1v8v.png)

完成这步后，站点（仓库）的导入过程就完成了。

## 设置侧边栏

导入站点后的下一个阶段是设置侧边栏菜单。你可以添加任意多个侧边栏菜单。不过，在这个例子中，我只添加一个侧边栏菜单。

导航到"Finish setup process" > "Set up sidebar"，然后点击"Configure sitebar"

![Forestry 欢迎界面](https://res.cloudinary.com/noezectz/v1663740974/astro-paper/forestry-io_4_j35uk9.png)

然后，点击"Add Section"按钮。

![点击'Add Section'添加侧边栏](https://res.cloudinary.com/noezectz/v1663741011/astro-paper/forestry-io_5_sxtgvx.png)

之后，为 Section Type 选择 DIRECTORY。

![选择'DIRECTORY'作为 Section Type](https://res.cloudinary.com/noezectz/v1663741052/astro-paper/forestry-io_6_lddmkx.png)

然后，配置目录部分。你可以按照我的设置来操作。

![配置目录部分](https://res.cloudinary.com/noezectz/v1663741105/astro-paper/forestry-io_7_jkwgi1.png)

完成这一步后，你应该能看到一个"Blog Posts"侧边栏菜单和一些博客文章。

## 设置媒体导入

在 Forestry CMS 中，你可以为媒体（又称资源）设置不同的选项，比如 Cloudinary、git commit media 等。我通常在 [Cloudinary](https://cloudinary.com/) 存储我的资源。要设置媒体导入，请转到 Settings > Media。然后选择你的图片存储提供商。（我选择了 Cloudinary）。

![设置'Cloudinary'作为媒体导入](https://res.cloudinary.com/noezectz/v1663741636/astro-paper/forestry-io-media-import_1_f8i4lm.png)

你可以在 [Forestry 文档](https://forestry.io/docs/media/cloudinary/)中查看 Forestry Cloudinary 设置的详细信息。

## 设置 Front matter 模板

完成所有设置后，你可以为将来的博客文章设置 front matter 模板。要设置 front matter 模板，请导航到侧边栏的"Front matter"菜单。

然后，点击右上角的"Add Template"按钮。

![Front Matter 模板页面](https://res.cloudinary.com/noezectz/v1663742060/astro-paper/forestry-io-frontmatter_yskfvn.png)

基于现有文档选择新模板。

![基于现有文档创建新模板](https://res.cloudinary.com/noezectz/v1663742179/astro-paper/forestry-io-existing-doc_bwcb9q.png)

然后，添加模板名称并选择一个文档页面作为模板。

作为最后的设置，在 front matter 字段设置中进行一些调整。

![在 front matter 字段设置中进行调整](https://res.cloudinary.com/noezectz/v1663742450/astro-paper/forestry-io-fm-config_jqmgwz.png)

以下是你需要进行的一些调整。

**_title_**

- Validation => REQUIRED => true

**_author_**

- Default => 你的名字

**_datetime_**

- Default => USE "NOW" AS DEFAULT

**_description_**

- Validation => REQUIRED => true

## 结论

现在你可以发布文章，写任何你想写的内容了。
