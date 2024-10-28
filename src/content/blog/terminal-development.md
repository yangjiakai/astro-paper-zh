---
title: 我如何使用 React 开发我的终端风格作品集网站
author: Sat Naing
pubDatetime: 2022-06-09T03:42:51Z
slug: how-do-i-develop-my-terminal-portfolio-website-with-react
featured: false
draft: false
tags:
  - JavaScript
  - ReactJS
  - ContextAPI
  - Styled-Components
  - TypeScript
description:
  "示例文章：使用 ReactJS、TypeScript 和 Styled-Components 开发一个终端风格的网站。
  包含自动完成、多主题、命令提示等功能。"
---

> 本文最初发表于我的[博客文章](https://satnaing.dev/blog/posts/how-do-i-develop-my-terminal-portfolio-website-with-react)。我放这篇文章是为了演示如何使用 AstroPaper 主题写博客文章。

使用 ReactJS、TypeScript 和 Styled-Components 开发一个终端风格的网站。包含自动完成、多主题、命令提示等功能。

[图片：Sat Naing 的终端风格作品集]

## 目录

## 简介

最近，我开发并发布了我的作品集网站和博客。我很高兴收到了一些好评。今天，我想介绍我的新终端风格作品集网站。它是使用 ReactJS 和 TypeScript 开发的。这个想法来自于 CodePen 和 YouTube。

## 技术栈

这是一个没有后端代码的前端项目。UI/UX 部分在 Figma 中设计。对于前端用户界面，我选择了 React 而不是原生 JavaScript 和 NextJS。为什么？

- 首先，我想写声明式代码。使用 JavaScript 命令式地管理 HTML DOM 真的很繁琐。
- 其次，因为这是 React！！！它快速且可靠。
- 最后，我不需要 NextJS 提供的 SEO 功能、路由和图片优化。

当然还有用于类型检查的 TypeScript。

在样式方面，我采用了一个与平常不同的方法。我没有选择纯 CSS、Sass 或像 TailwindCSS 这样的实用工具 CSS 框架，而是选择了 CSS-in-JS 方式（Styled-Components）。虽然我已经知道 Styled-Components 有一段时间了，但我从未尝试过。所以，这个项目中 Styled-Components 的写作风格和结构可能不是很有组织或很好。

这个项目不需要很复杂的状态管理。我只在这个项目中使用 ContextAPI 来实现多主题和避免 prop drilling。

以下是技术栈的快速回顾：

- 前端：[ReactJS](https://reactjs.org/ "React 网站")、[TypeScript](https://www.typescriptlang.org/ "TypeScript 网站")
- 样式：[Styled-Components](https://styled-components.com/ "Styled-Components 网站")
- UI/UX：[Figma](https://figma.com/ "Figma 网站")
- 状态管理：[ContextAPI](https://reactjs.org/docs/context.html "React ContextAPI")
- 部署：[Netlify](https://www.netlify.com/ "Netlify 网站")

## 功能特性

以下是该项目的一些功能特性。

### 多主题

用户可以切换多个主题。在写这篇文章时，有5种主题；未来可能会添加更多主题。选择的主题会保存在本地存储中，这样页面刷新后主题就不会改变。

![设置不同主题](https://i.ibb.co/fSTCnWB/terminal-portfolio-multiple-themes.gif)

### 命令行自动补全

为了尽可能接近真实终端的外观和体验，我添加了命令行自动补全功能，只需按"Tab"或"Ctrl + i"就可以自动填充部分输入的命令。

![演示命令行自动补全](https://i.ibb.co/CQTGGLF/terminal-autocomplete.gif)

### 历史命令

用户可以通过按上下方向键返回到之前的命令或浏览之前输入的命令。

![使用向上箭头回到之前的命令](https://i.ibb.co/vD1pSRv/terminal-up-down.gif)

### 查看/清除命令历史

可以通过在命令行中输入"history"来查看之前输入的命令。通过输入"clear"或按"Ctrl + l"可以清除所有命令历史和终端屏幕。

![使用'clear'或'Ctrl + L'命令清除终端](https://i.ibb.co/SJBy8Rr/terminal-clear.gif)

## 结语

这是一个非常有趣的项目，这个项目的一个特别之处在于我必须专注于逻辑而不是用户界面（尽管这某种程度上是一个前端项目）。

## 项目链接

- 网站：[https://terminal.satnaing.dev/](https://terminal.satnaing.dev/ "https://terminal.satnaing.dev/")
- 代码仓库：[https://github.com/satnaing/terminal-portfolio](https://github.com/satnaing/terminal-portfolio "https://github.com/satnaing/terminal-portfolio")
