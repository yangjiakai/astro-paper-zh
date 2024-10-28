# AstroPaper 📄

AstroPaper 是一个极简、响应式、无障碍且 SEO 友好的 Astro 博客主题。这个主题是基于[我的个人博客](https://satnaing.dev/blog)设计和制作的。

该主题遵循最佳实践，默认提供无障碍功能。默认支持浅色和深色模式。此外，还可以配置其他配色方案。

这个主题是自文档化的 —— 这意味着主题中的文章/帖子也可以被视为文档。阅读[博客文章](https://astro-paper.pages.dev/posts/)或查看 [README 文档部分](#-documentation)了解更多信息。

## 🔥 特性

- [x] 类型安全的 markdown
- [x] 超快的性能
- [x] 无障碍访问(键盘/VoiceOver)
- [x] 响应式设计(移动设备~桌面)
- [x] SEO 友好
- [x] 明暗模式
- [x] 模糊搜索
- [x] 草稿文章 & 分页
- [x] 站点地图 & RSS 订阅
- [x] 遵循最佳实践
- [x] 高度可定制
- [x] 博客文章动态 OG 图片生成 [#15](https://github.com/satnaing/astro-paper/pull/15) ([博客文章](https://astro-paper.pages.dev/posts/dynamic-og-image-generation-in-astropaper-blog-posts/))

_注意：我已经使用 Mac 上的 **VoiceOver** 和 Android 上的 **TalkBack** 测试了 AstroPaper 的屏幕阅读器可访问性。我无法测试所有其他屏幕阅读器。不过，AstroPaper 的无障碍增强功能在其他设备上也应该运行良好。_

## ✅ Lighthouse 得分

<p align="center">
  <a href="https://pagespeed.web.dev/report?url=https%3A%2F%2Fastro-paper.pages.dev%2F&form_factor=desktop">
    <img width="710" alt="AstroPaper Lighthouse Score" src="AstroPaper-lighthouse-score.svg">
  <a>
</p>

## 🚀 项目结构

在 AstroPaper 中，你会看到以下文件夹和文件：

```bash
/
├── public/
│   ├── assets/
│   │   └── logo.svg
│   │   └── logo.png
│   └── favicon.svg
│   └── astropaper-og.jpg
│   └── robots.txt
│   └── toggle-theme.js
├── src/
│   ├── assets/
│   │   └── socialIcons.ts
│   ├── components/
│   ├── content/
│   │   |  blog/
│   │   |    └── some-blog-posts.md
│   │   └── config.ts
│   ├── layouts/
│   └── pages/
│   └── styles/
│   └── utils/
│   └── config.ts
│   └── types.ts
└── package.json
```

Astro 会在 `src/pages/` 目录中查找 `.astro` 或 `.md` 文件。每个页面都会根据其文件名暴露为一个路由。

任何静态资源，如图片，都可以放在 `public/` 目录中。

所有博客文章都存储在 `src/content/blog` 目录中。

## 📖 文档

文档可以通过两种格式阅读：_markdown_ 和 _博客文章_。

- 配置 - [markdown](src/content/blog/how-to-configure-astropaper-theme.md) | [博客文章](https://astro-paper.pages.dev/posts/how-to-configure-astropaper-theme/)
- 添加文章 - [markdown](src/content/blog/adding-new-post.md) | [博客文章](https://astro-paper.pages.dev/posts/adding-new-posts-in-astropaper-theme/)
- 自定义配色方案 - [markdown](src/content/blog/customizing-astropaper-theme-color-schemes.md) | [博客文章](https://astro-paper.pages.dev/posts/customizing-astropaper-theme-color-schemes/)
- 预定义配色方案 - [markdown](src/content/blog/predefined-color-schemes.md) | [博客文章](https://astro-paper.pages.dev/posts/predefined-color-schemes/)

> 对于 AstroPaper v1，请查看[这个分支](https://github.com/satnaing/astro-paper/tree/astro-paper-v1)和这个[在线地址](https://astro-paper-v1.astro-paper.pages.dev/)

## 💻 技术栈

**主框架** - [Astro](https://astro.build/)  
**类型检查** - [TypeScript](https://www.typescriptlang.org/)  
**组件框架** - [ReactJS](https://reactjs.org/)  
**样式** - [TailwindCSS](https://tailwindcss.com/)  
**UI/UX** - [Figma 设计文件](https://www.figma.com/community/file/1356898632249991861)  
**模糊搜索** - [FuseJS](https://fusejs.io/)  
**图标** - [Boxicons](https://boxicons.com/) | [Tablers](https://tabler-icons.io/)  
**代码格式化** - [Prettier](https://prettier.io/)  
**部署** - [Cloudflare Pages](https://pages.cloudflare.com/)  
**关于页面插图** - [https://freesvgillustration.com](https://freesvgillustration.com/)  
**代码检查** - [ESLint](https://eslint.org)

## 👨🏻‍💻 本地运行

你可以通过在所需目录中运行以下命令来开始使用这个项目：

```bash
# npm 6.x
npm create astro@latest --template satnaing/astro-paper

# npm 7+，需要额外的双横线：
npm create astro@latest -- --template satnaing/astro-paper

# yarn
yarn create astro --template satnaing/astro-paper

# pnpm
pnpm dlx create-astro --template satnaing/astro-paper
```

> **_警告！_** 如果你使用的是 `yarn 1`，你可能需要[安装 `sharp`](https://sharp.pixelplumbing.com/install) 作为依赖项。

然后通过运行以下命令启动项目：

```bash
# 安装依赖
npm run install

# 启动项目
npm run dev
```

作为替代方案，如果你已安装 Docker，可以使用 Docker 在本地运行此项目。方法如下：

```bash
# 构建 Docker 镜像
docker build -t astropaper .

# 运行 Docker 容器
docker run -p 4321:80 astropaper
```

## Google 站点验证（可选）

你可以使用环境变量在 AstroPaper 中轻松添加 [Google 站点验证 HTML 标签](https://support.google.com/webmasters/answer/9008080#meta_tag_verification&zippy=%2Chtml-tag)。这一步是可选的。如果你不添加以下环境变量，google-site-verification 标签将不会出现在 HTML 的 `<head>` 部分。

```bash
# 在你的环境变量文件中 (.env)
PUBLIC_GOOGLE_SITE_VERIFICATION=你的-google-站点验证-值
```

> 查看[这个讨论](https://github.com/satnaing/astro-paper/discussions/334#discussioncomment-10139247)了解如何将 AstroPaper 添加到 Google Search Console。

## 🧞 命令

所有命令都从项目根目录的终端运行：

> **_注意！_** 对于 `Docker` 命令，我们必须在机器上[安装](https://docs.docker.com/engine/install/)它。

| 命令                                 | 操作                                                                                                               |
| :----------------------------------- | :----------------------------------------------------------------------------------------------------------------- |
| `npm install`                        | 安装依赖                                                                                                           |
| `npm run dev`                        | 在 `localhost:4321` 启动本地开发服务器                                                                             |
| `npm run build`                      | 构建生产站点到 `./dist/`                                                                                           |
| `npm run preview`                    | 在部署前本地预览构建                                                                                               |
| `npm run format:check`               | 使用 Prettier 检查代码格式                                                                                         |
| `npm run format`                     | 使用 Prettier 格式化代码                                                                                           |
| `npm run sync`                       | 为所有 Astro 模块生成 TypeScript 类型。[了解更多](https://docs.astro.build/en/reference/cli-reference/#astro-sync) |
| `npm run lint`                       | 使用 ESLint 进行代码检查                                                                                           |
| `docker compose up -d`               | 在 docker 上运行 AstroPaper，你可以使用与 `dev` 命令相同的主机名和端口访问                                         |
| `docker compose run app npm install` | 你可以在 docker 容器中运行上述任何命令                                                                             |
| `docker build -t astropaper .`       | 构建 AstroPaper 的 Docker 镜像                                                                                     |
| `docker run -p 4321:80 astropaper`   | 在 Docker 上运行 AstroPaper。网站将在 `http://localhost:4321` 上可访问                                             |

> **_警告！_** Windows PowerShell 用户如果想要在开发期间[运行诊断](https://docs.astro.build/en/reference/cli-reference/#astro-check)（`astro check --watch & astro dev`），可能需要安装 [concurrently 包](https://www.npmjs.com/package/concurrently)。更多信息，请参见[此问题](https://github.com/satnaing/astro-paper/issues/113)。

## ✨ 反馈 & 建议

如果你有任何建议/反馈，可以通过[我的邮箱](mailto:contact@satnaing.dev)联系我。或者，如果你发现错误或想要请求新功能，随时可以开启一个 issue。

## 📜 许可证

基于 MIT 许可证授权，版权所有 © 2023

---

由 [Sat Naing](https://satnaing.dev) 👨🏻‍💻 和[贡献者们](https://github.com/satnaing/astro-paper/graphs/contributors)用 🤍 制作。
