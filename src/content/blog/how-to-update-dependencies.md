---
title: 如何更新 AstroPaper 的依赖项
author: Sat Naing
pubDatetime: 2023-07-20T15:33:05.569Z
slug: how-to-update-dependencies
featured: false
draft: false
ogImage: /assets/forrest-gump-quote.webp
tags:
  - FAQ
description: 如何更新项目依赖项和 AstroPaper 模板。
---

更新项目的依赖项可能会很繁琐。然而，忽视项目依赖项的更新也不是一个好主意 😬。在这篇文章中，我将分享我通常如何更新我的项目，以 AstroPaper 为例。不过，这些步骤也适用于其他 js/node 项目。

![Forrest Gump 假引用](/assets/forrest-gump-quote.webp)

## 目录

## 更新包依赖项

有几种方法可以更新依赖项，我尝试过各种方法来找到最简单的途径。其中一种方法是使用 `npm install package-name@latest` 手动更新每个包。这种方法是最直接的更新方式。但是，这可能不是最有效的选择。

我推荐使用 [npm-check-updates 包](https://www.npmjs.com/package/npm-check-updates)来更新依赖项。freeCodeCamp 有一篇很好的[文章](https://www.freecodecamp.org/news/how-to-update-npm-dependencies/)介绍了这个工具，所以我不会详细解释它是什么以及如何使用。相反，我会向你展示我的典型方法。

首先，全局安装 `npm-check-updates` 包。

```bash
npm install -g npm-check-updates
```

在进行任何更新之前，最好检查一下所有可以更新的新依赖项。

```bash
ncu
```

大多数情况下，补丁依赖项可以在不影响项目的情况下更新。所以，我通常通过运行 `ncu -i --target patch` 或 `ncu -u --target patch` 来更新补丁依赖项。区别在于 `ncu -u --target patch` 将更新所有补丁，而 `ncu -i --target patch` 将提供选项让你选择要更新哪个包。由你决定采用哪种方式。

下一部分涉及更新次要依赖项。次要包更新通常不会破坏项目，但最好还是查看相应包的发布说明。这些次要更新通常包含一些可以应用到我们项目中的新功能。

```bash
ncu -i --target minor
```

最后但同样重要的是，依赖项中可能有一些主要包更新。所以，通过运行以下命令检查剩余的依赖项更新

```bash
ncu -i
```

如果有任何主要更新（或者你还需要进行的一些更新），上述命令将输出这些剩余的包。如果包是主要版本更新，你必须非常小心，因为这很可能会破坏整个项目。因此，请非常仔细地阅读相应的发布说明（或）文档，并相应地进行更改。

如果你运行 `ncu -i` 并发现没有更多需要更新的包，_**恭喜!!!**_ 你已经成功更新了项目中的所有依赖项。

## 更新 AstroPaper 模板

与其他开源项目一样，AstroPaper 也在不断发展，包括错误修复、功能更新等。所以如果你是使用 AstroPaper 作为模板的用户，当有新版本发布时，你可能也想更新模板。

问题是，你可能已经根据自己的喜好更新了模板。因此，我不能准确地展示**"适用于所有人的完美方式"**来将模板更新到最新版本。不过，这里有一些在不破坏你的仓库的情况下更新模板的提示。请记住，大多数情况下，更新包依赖项可能就足够了。

### 需要注意的文件和目录

在大多数情况下，你可能不想覆盖的文件和目录（因为你可能已经更新了这些文件）是 `src/content/blog/`、`src/config.ts`、`src/pages/about.md` 以及其他资源和样式，如 `public/` 和 `src/styles/base.css`。

如果你是一个只更新模板基本内容的人，那么除了上述文件和目录外，用最新的 AstroPaper 替换所有内容应该没问题。这就像纯 Android 操作系统和其他厂商特定的操作系统（如 OneUI）一样。你对基础的修改越少，需要更新的就越少。

你可以手动一个一个替换每个文件，或者你可以使用 git 的魔力来更新所有内容。我不会向你展示手动替换过程，因为它非常直接。如果你对这种直接但效率低下的方法不感兴趣，请继续往下看 🐻。

### 使用 Git 更新 AstroPaper

**重要提示!!!**

> 只有在你知道如何解决合并冲突的情况下才执行以下操作。否则，你最好手动替换文件或只更新依赖项。

首先，在你的项目中添加 astro-paper 作为远程仓库。

```bash
git remote add astro-paper https://github.com/satnaing/astro-paper.git
```

检出到一个新分支以更新模板。如果你知道自己在做什么，并且对自己的 git 技能有信心，可以省略这一步。

```bash
git checkout -b build/update-astro-paper
```

然后，通过运行以下命令从 astro-paper 拉取更改

```bash
git pull astro-paper main
```

如果遇到 `fatal: refusing to merge unrelated histories` 错误，可以通过运行以下命令解决

```bash
git pull astro-paper main --allow-unrelated-histories
```

运行上述命令后，你可能会在项目中遇到冲突。你需要手动解决这些冲突，并根据你的需求进行必要的调整。

解决冲突后，彻底测试你的博客以确保一切正常运行。检查你的文章、组件和任何自定义内容。

一旦你对结果满意，就可以将更新分支合并到你的主分支中（仅当你在另一个分支中更新模板时）。恭喜！你已经成功将模板更新到最新版本。你的博客现在已经是最新的，可以大放异彩了！🎉

## 结论

在这篇文章中，我分享了一些关于更新依赖项和 AstroPaper 模板的见解和流程。我真诚地希望这篇文章能够证明其价值，并帮助你更有效地管理项目。

如果你有任何更新依赖项/AstroPaper 的替代或改进方法，我很乐意听取你的意见。因此，请不要犹豫，在仓库中开始讨论，给我发邮件，或者提出问题。非常感谢你的意见和想法！

请理解，这些天我的日程安排很紧，可能无法快速回复。但是，我保证会尽快回复你。😬

感谢你花时间阅读这篇文章，祝你的项目一切顺利！
