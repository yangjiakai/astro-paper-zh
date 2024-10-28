---
author: Sat Naing
pubDatetime: 2022-09-23T15:22:00Z
modDatetime: 2023-07-21T10:11:06.130Z
title: 如何在 AstroPaper 中添加预计阅读时间
slug: how-to-add-estimated-reading-time
featured: false
draft: false
tags:
  - FAQ
description: 如何在 AstroPaper 的博客文章中添加"预计阅读时间"功能。
---

正如 [Astro 文档](https://docs.astro.build/en/recipes/reading-time/) 所说，我们可以使用 remark 插件在 frontmatter 中添加阅读时间属性。但是由于某些原因，我们无法按照 Astro 文档中所述的方式添加此功能。因此，我们需要做一些调整。这篇文章将演示如何实现这一点。

## 目录

## 在 PostDetails 中添加阅读时间

步骤 (1) 安装必需的依赖。

```bash
npm install reading-time mdast-util-to-string
```

步骤 (2) 在 `utils` 目录下创建 `remark-reading-time.mjs` 文件

```js
import getReadingTime from "reading-time";
import { toString } from "mdast-util-to-string";

export function remarkReadingTime() {
  return function (tree, { data }) {
    const textOnPage = toString(tree);
    const readingTime = getReadingTime(textOnPage);
    // readingTime.text 将给我们一个友好的字符串形式的阅读时间
    // 例如 "3 min read"
    data.astro.frontmatter.minutesRead = readingTime.text;
  };
}
```

步骤 (3) 将插件添加到 `astro.config.ts` 中

```js
import { remarkReadingTime } from "./src/utils/remark-reading-time.mjs"; // 确保相对路径正确

// https://astro.build/config
export default defineConfig({
  site: SITE.website,
  integrations: [
    // 其他集成
  ],
  markdown: {
    remarkPlugins: [
      remarkToc,
      remarkReadingTime, // 👈🏻 我们的插件
      [
        remarkCollapse,
        {
          test: "Table of contents",
        },
      ],
    ],
    // 其他配置
  },
  // 其他配置
});
```

步骤 (4) 在博客模式中添加 `readingTime` (`src/content/config.ts`)

```ts
import { SITE } from "@config";
import { defineCollection, z } from "astro:content";

const blog = defineCollection({
  type: "content",
  schema: ({ image }) =>
    z.object({
      // 其他...
      canonicalURL: z.string().optional(),
      readingTime: z.string().optional(), // 👈🏻 readingTime frontmatter
    }),
});

export const collections = { blog };
```

步骤 (5) 在 `src/utils` 目录下创建一个名为 `getPostsWithRT.ts` 的新文件。

```ts
import type { CollectionEntry } from "astro:content";
import { slugifyStr } from "./slugify";

interface Frontmatter {
  frontmatter: {
    title: string;
    minutesRead: string;
  };
}

export const getReadingTime = async () => {
  // 使用 glob 获取所有文章。这是为了获取更新后的 frontmatter
  const globPosts = import.meta.glob<Frontmatter>("../content/blog/*.md");

  // 然后，在 JS Map 中设置这些 frontmatter 值的键值对
  const mapFrontmatter = new Map();
  const globPostsValues = Object.values(globPosts);
  await Promise.all(
    globPostsValues.map(async globPost => {
      const { frontmatter } = await globPost();
      mapFrontmatter.set(
        slugifyStr(frontmatter.title),
        frontmatter.minutesRead
      );
    })
  );

  return mapFrontmatter;
};

const getPostsWithRT = async (posts: CollectionEntry<"blog">[]) => {
  const mapFrontmatter = await getReadingTime();
  return posts.map(post => {
    post.data.readingTime = mapFrontmatter.get(slugifyStr(post.data.title));
    return post;
  });
};

export default getPostsWithRT;
```

步骤 (6) 按如下方式重构 `/src/pages/posts/[slug]/index.astro` 中的 `getStaticPaths`

```ts
---
// 其他导入
import getPostsWithRT from "@utils/getPostsWithRT";

export interface Props {
  post: CollectionEntry<"blog">;
}

export async function getStaticPaths() {
  const posts = await getCollection("blog", ({ data }) => !data.draft);

  const postsWithRT = await getPostsWithRT(posts); // 用这个函数替换阅读时间逻辑

   const postResult = postsWithRT.map(post => ({ // 确保用 postsWithRT 替换 posts
    params: { slug: post.slug },
    props: { post },
  }));

// 其他代码
```

步骤 (7) 像这样重构 `PostDetails.astro`。现在你可以在 `PostDetails.astro` 中访问和显示 `readingTime` 了

```ts
---
// 导入

export interface Props {
  post: CollectionEntry<"blog">;
}

const { post } = Astro.props;

const {
  title,
  author,
  description,
  ogImage,
  readingTime, // 现在我们可以直接从 frontmatter 访问 readingTime
  pubDatetime,
  modDatetime,
  tags } = post.data;

// 其他代码
---
```

## 在 PostDetails 之外访问阅读时间（可选）

通过遵循前面的步骤，你现在可以在文章详情页面访问 `readingTime` frontmatter 属性。有时这正是你想要的。如果是这样，你可以跳过下一节。但是，如果你想在首页、文章列表页面等任何地方显示"预计阅读时间"，你需要执行以下额外步骤。

步骤 (1) 按如下方式更新 `utils/getSortedPosts.ts`

```ts
import type { CollectionEntry } from "astro:content";
import getPostsWithRT from "./getPostsWithRT";

const getSortedPosts = async (posts: CollectionEntry<"blog">[]) => {
  // 确保这个函数是异步的
  const postsWithRT = await getPostsWithRT(posts); // 添加阅读时间
  return postsWithRT
    .filter(({ data }) => !data.draft)
    .sort(
      (a, b) =>
        Math.floor(
          new Date(b.data.modDatetime ?? b.data.pubDatetime).getTime() / 1000
        ) -
        Math.floor(
          new Date(a.data.modDatetime ?? a.data.pubDatetime).getTime() / 1000
        )
    );
};

export default getSortedPosts;
```

步骤 (2) 确保重构每个使用 `getSortedPosts` 函数的文件。你只需在 `getSortedPosts` 函数前面添加 `await` 关键字。

使用 `getSortedPosts` 函数的文件如下：

- src/pages/index.astro
- src/pages/search.astro
- src/pages/rss.xml.ts
- src/pages/posts/index.astro
- src/pages/posts/[slug]/index.astro
- src/utils/getPostsByTag.ts

你需要做的就是这样：

```ts
const sortedPosts = getSortedPosts(posts); // 旧代码 ❌
const sortedPosts = await getSortedPosts(posts); // 新代码 ✅
```

现在，`getPostsByTag` 函数变成了一个异步函数。因此，我们也需要 `await` `getPostsByTag` 函数。

- src/pages/tags/[tag]/[page].astro
- src/pages/tags/[tag]/index.astro

```ts
const postsByTag = getPostsByTag(posts, tag); // 旧代码 ❌
const postsByTag = await getPostsByTag(posts, tag); // 新代码 ✅
```

此外，像这样更新 `src/pages/tags/[tag]/[page].astro` 中的 `getStaticPaths`：

```ts
export async function getStaticPaths() {
  const posts = await getCollection("blog");

  const tags = getUniqueTags(posts);

  // 确保等待 promises
  const paths = await Promise.all(
    tags.map(async ({ tag, tagName }) => {
      const tagPosts = await getPostsByTag(posts, tag);
      const totalPages = getPageNumbers(tagPosts.length);

      return totalPages.map(page => ({
        params: { tag, page: String(page) },
        props: { tag, tagName },
      }));
    })
  );

  return paths.flat(); // 展平数组
}
```

现在你可以在 `PostDetails` 之外的其他地方访问 `readingTime` 了

## 显示阅读时间（可选）

既然你现在可以在文章详情页（或如果你完成了上一节，则可以在任何地方）访问 `readingTime`，你可以根据需要在任何地方显示 `readingTime`。

但在本节中，我将向你展示如何在组件中显示 `readingTime`。这是可选的。如果你愿意，可以跳过这一节。

步骤 (1) 更新 `Datetime` 组件以显示 `readingTime`

```tsx
import { LOCALE } from "@config";

export interface Props {
  datetime: string | Date;
  size?: "sm" | "lg";
  className?: string;
  readingTime?: string; // 新类型
}

export default function Datetime({
  datetime,
  size = "sm",
  className,
  readingTime, // 新属性
}: Props) {
  return (
    // 其他代码
    <span className={`italic ${size === "sm" ? "text-sm" : "text-base"}`}>
      <FormattedDatetime pubDatetime={pubDatetime} modDatetime={modDatetime} />
      <span> ({readingTime})</span> {/* 显示阅读时间 */}
    </span>
    // 其他代码
  );
}
```

步骤 (2) 然后，从父组件传递 `readingTime` 属性。

文件：Card.tsx

```ts
export default function Card({ href, frontmatter, secHeading = true }: Props) {
  const { title, pubDatetime, modDatetime description, readingTime } = frontmatter;
  return (
    ...
    <Datetime
      pubDatetime={pubDatetime}
      modDatetime={modDatetime}
      readingTime={readingTime}
    />
    ...
  );
}
```

文件：PostDetails.tsx

```jsx
// 其他代码
<main id="main-content">
  <h1 class="post-title">{title}</h1>
  <Datetime
    pubDatetime={pubDatetime}
    modDatetime={modDatetime}
    size="lg"
    className="my-2"
    readingTime={readingTime}
  />
  {/* 其他代码 */}
</main>
// 其他代码
```

## 结论

通过遵循提供的步骤和调整，你现在可以在你的内容中加入这个有用的功能。我希望这篇文章能帮助你在博客中添加 `readingTime`。AstroPaper 可能会在未来的版本中默认包含阅读时间。🤷🏻‍♂️

感谢阅读 🙏🏻
