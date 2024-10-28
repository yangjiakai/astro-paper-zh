---
author: Alberto Perdomo
pubDatetime: 2024-09-08T20:58:52.737Z
title: 在 AstroPaper 博客文章中添加 LaTeX 公式
featured: false
tags:
  - rendering
  - docs
description: 如何在 AstroPaper 的 Markdown 文件中使用 LaTeX 公式。
---

本文档演示了如何在 AstroPaper 的 Markdown 文件中使用 LaTeX 公式。LaTeX 是一个强大的排版系统，常用于数学和科学文档。

## 目录

## 使用说明

在本节中，你将了解如何在 AstroPaper 的 Markdown 文件中添加 LaTeX 支持。

1. 运行 `npm install rehype-katex remark-math katex` 安装必要的 remark 和 rehype 插件。

2. 更新 Astro 配置文件（`astro.config.ts`）以使用这些插件：

```ts
// 其他导入
import remarkMath from "remark-math";
import rehypeKatex from "rehype-katex";

export default defineConfig({
  // 其他配置
  markdown: {
    remarkPlugins: [
      remarkMath,
      remarkToc,
      [
        remarkCollapse,
        {
          test: "Table of contents",
        },
      ],
    ],
    rehypePlugins: [rehypeKatex],
    // 其他 markdown 配置
  },
  // 其他配置
});
```

3. 在主布局文件 `src/layouts/Layout.astro` 中导入 KaTeX CSS

```astro
---
import { LOCALE, SITE } from "@config";

// astro 代码
---

<!doctype html>
<!-- 其他部分... -->
<script is:inline src="/toggle-theme.js"></script>
<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/npm/katex@0.15.2/dist/katex.min.css"
/>

<body>
  <slot />
</body>
```

这样就完成了，这个设置允许你在 Markdown 文件中编写 LaTeX 公式，这些公式在站点构建时会被正确渲染。完成设置后，文档的其余部分将会正确显示。

## 行内公式

行内公式写在单个美元符号 `$...$` 之间。这里有一些例子：

1. 著名的质能等价公式：`$E = mc^2$`
2. 二次方程求根公式：`$x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$`
3. 欧拉恒等式：`$e^{i\pi} + 1 = 0$`

## 块级公式

对于更复杂的公式，或当你想要公式单独显示在一行时，使用双美元符号 `$$...$$`：

高斯积分：

```bash
$$ \int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi} $$
```

黎曼 zeta 函数的定义：

```bash
$$ \zeta(s) = \sum_{n=1}^{\infty} \frac{1}{n^s} $$
```

麦克斯韦方程组的微分形式：

```bash
$$
\begin{aligned}
\nabla \cdot \mathbf{E} &= \frac{\rho}{\varepsilon_0} \\
\nabla \cdot \mathbf{B} &= 0 \\
\nabla \times \mathbf{E} &= -\frac{\partial \mathbf{B}}{\partial t} \\
\nabla \times \mathbf{B} &= \mu_0\left(\mathbf{J} + \varepsilon_0 \frac{\partial \mathbf{E}}{\partial t}\right)
\end{aligned}
$$
```

## 使用数学符号

LaTeX 提供了广泛的数学符号：

- 希腊字母：`$\alpha$`、`$\beta$`、`$\gamma$`、`$\delta$`、`$\epsilon$`、`$\pi$`
- 运算符：`$\sum$`、`$\prod$`、`$\int$`、`$\partial$`、`$\nabla$`
- 关系符号：`$\leq$`、`$\geq$`、`$\approx$`、`$\sim$`、`$\propto$`
- 逻辑符号：`$\forall$`、`$\exists$`、`$\neg$`、`$\wedge$`、`$\vee$`
