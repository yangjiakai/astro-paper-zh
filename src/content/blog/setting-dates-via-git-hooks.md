---
title: 如何使用 Git Hooks 设置创建和修改日期
author: Simon Smale
pubDatetime: 2024-01-03T20:40:08Z
modDatetime: 2024-01-08T18:59:05Z
featured: false
draft: false
tags:
  - docs
  - FAQ
canonicalURL: https://smale.codes/posts/setting-dates-via-git-hooks/
description: 如何在 AstroPaper 中使用 Git Hooks 设置创建和修改日期
---

在这篇文章中，我将解释如何使用 pre-commit Git hook 来自动设置 AstroPaper 博客主题 frontmatter 中的创建时间(`pubDatetime`)和修改时间(`modDatetime`)。

## 目录

## 让它无处不在

[Git hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks) 非常适合用来自动化一些任务，比如[添加](https://gist.github.com/SSmale/3b380e5bbed3233159fb7031451726ea)或[检查](https://itnext.io/using-git-hooks-to-enforce-branch-naming-policy-ffd81fa01e5e)分支名称到提交信息中，或者[防止提交明文密码](https://gist.github.com/SSmale/367deee757a9b2e119d241e120249000)。它们最大的缺点是客户端钩子是按机器设置的。

你可以通过创建一个 `hooks` 目录并手动将它们复制到 `.git/hooks` 目录或设置符号链接来解决这个问题，但这都需要你记得去设置，而这不是我擅长的事情。

由于这个项目使用 npm，我们可以使用一个叫做 [Husky](https://typicode.github.io/husky/)的包（AstroPaper 中已经安装）来自动安装这些钩子。

> 更新！在 AstroPaper [v4.3.0](https://github.com/satnaing/astro-paper/releases/tag/v4.3.0) 中，pre-commit hook 已被 GitHub Actions 取代。不过，你可以轻松地[自行安装 Husky](https://typicode.github.io/husky/get-started.html)。

## 钩子

因为我们希望这个钩子在我们提交代码时运行以更新日期，并将其作为我们更改的一部分，所以我们要使用 `pre-commit` 钩子。AstroPaper 项目已经设置好了这个，但如果没有的话，你可以运行 `npx husky add .husky/pre-commit 'echo "This is our new pre-commit hook"'`。

导航到 `hooks/pre-commit` 文件，我们将添加以下一个或两个代码片段。

### 当文件被编辑时更新修改日期

---

更新：

这部分已经更新为一个更智能的钩子版本。现在它只会在文章发布后才更新 `modDatetime`。在首次发布时，将 draft 状态设置为 `first`，然后看看魔法发生。

---

```shell
# 修改的文件，更新 modDatetime
git diff --cached --name-status |
grep -i '^M.*\.md$' |
while read _ file; do
  filecontent=$(cat "$file")
  frontmatter=$(echo "$filecontent" | awk -v RS='---' 'NR==2{print}')
  draft=$(echo "$frontmatter" | awk '/^draft: /{print $2}')
  if [ "$draft" = "false" ]; then
    echo "$file modDateTime updated"
    cat $file | sed "/---.*/,/---.*/s/^modDatetime:.*$/modDatetime: $(date -u "+%Y-%m-%dT%H:%M:%SZ")/" > tmp
    mv tmp $file
    git add $file
  fi
  if [ "$draft" = "first" ]; then
    echo "First release of $file, draft set to false and modDateTime removed"
    cat $file | sed "/---.*/,/---.*/s/^modDatetime:.*$/modDatetime:/" | sed "/---.*/,/---.*/s/^draft:.*$/draft: false/" > tmp
    mv tmp $file
    git add $file
  fi
done
```

`git diff --cached --name-status` 获取已暂存准备提交的文件。输出看起来像：

```shell
A       src/content/blog/setting-dates-via-git-hooks.md
```

开头的字母表示采取了什么操作，在上面的例子中文件被添加了。修改的文件有 `M`。

我们将该输出通过管道传递给 grep 命令，在这里我们查找已被修改的每一行。该行需要以 `M` 开头(`^(M)`)，后面跟任意数量的字符(`.*`)，并以 `.md` 文件扩展名结尾(`.(md)$`)。这将过滤掉不是被修改的 markdown 文件的行 `egrep -i "^(M).*\.(md)$"`。

---

#### 改进 - 更明确

这可以被添加为只查找 `blog` 目录中的 markdown 文件，因为只有这些文件会有正确的 frontmatter。

---

正则表达式将捕获两个部分，字母和文件路径。我们将这个列表通过管道传递到 while 循环中，遍历匹配的行并将字母赋值给 `a`，路径赋值给 `b`。我们暂时忽略 `a`。

要知道文件的草稿状态，我们需要它的 frontmatter。在下面的代码中，我们使用 `cat` 获取文件内容，然后使用 `awk` 在 frontmatter 分隔符(`---`)处分割文件并获取第二个块(frontmatter，即两个 `---` 之间的部分)。从这里我们再次使用 `awk` 找到 draft 键并打印其值。

```shell
  filecontent=$(cat "$file")
  frontmatter=$(echo "$filecontent" | awk -v RS='---' 'NR==2{print}')
  draft=$(echo "$frontmatter" | awk '/^draft: /{print $2}')
```

现在我们有了 `draft` 的值，我们将执行以下 3 种操作之一：设置 modDatetime 为现在(当 draft 为 false 时 `if [ "$draft" = "false" ]; then`)，清除 modDatetime 并设置 draft 为 false(当 draft 设置为 first 时 `if [ "$draft" = "first" ]; then`)，或者什么都不做(在任何其他情况下)。

接下来的 sed 命令对我来说有点神奇，因为我不经常使用它，它是从[另一篇做类似事情的博客文章](https://mademistakes.com/notes/adding-last-modified-timestamps-with-git/)中复制的。简单来说，它在文件的 frontmatter 标签(`---`)中查找 `pubDatetime:` 键，获取整行并用相同的键和正确格式的当前日期时间 `pubDatetime: $(date -u "+%Y-%m-%dT%H:%M:%SZ")/"` 替换它。

这个替换是在整个文件的上下文中进行的，所以我们把它放到一个临时文件中(`> tmp`)，然后将新文件移动(`mv`)到旧文件的位置，覆盖它。然后将其添加到 git 中，准备提交，就好像我们自己做了这个更改一样。

---

#### 注意

为了让 `sed` 工作，frontmatter 中需要已经有 `modDatetime` 键。为了让应用程序能够使用空日期构建，你需要做一些其他更改，请参见[下文](#empty-moddatetime-changes)。

---

### 为新文件添加日期

为新文件添加日期的过程与上面相同，但这次我们查找已添加的行(`A`)，并替换 `pubDatetime` 值。

```shell
# 新文件，添加/更新 pubDatetime
git diff --cached --name-status | egrep -i "^(A).*\.(md)$" | while read a b; do
  cat $b | sed "/---.*/,/---.*/s/^pubDatetime:.*$/pubDatetime: $(date -u "+%Y-%m-%dT%H:%M:%SZ")/" > tmp
  mv tmp $b
  git add $b
done
```

---

#### 改进 - 只循环一次

我们可以在循环中使用 `a` 变量来切换，在一个循环中更新 `modDatetime` 或添加 `pubDatetime`。

---

## 填充 frontmatter

如果你的 IDE 支持代码片段，那么可以创建一个自定义代码片段来填充 frontmatter。[AstroPaper v4 将默认为 VSCode 提供一个。](https://github.com/satnaing/astro-paper/pull/206)

<video autoplay muted="muted" controls plays-inline="true" class="border border-skin-line">
  <source src="https://github.com/satnaing/astro-paper/assets/17761689/e13babbc-2d78-405d-8758-ca31915e41b0" type="video/mp4">
</video>

## 空 `modDatetime` 更改

为了让 Astro 编译 markdown 并完成其工作，它需要知道 frontmatter 中预期的内容。这是通过 `src/content/config.ts` 中的配置来完成的。

要允许键存在但没有值，我们需要编辑第 10 行来添加 `.nullable()` 函数。

```typescript
const blog = defineCollection({
  type: "content",
  schema: ({ image }) =>
    z.object({
      author: z.string().default(SITE.author),
      pubDatetime: z.date(),
-     modDatetime: z.date().optional(),
+     modDatetime: z.date().optional().nullable(),
      title: z.string(),
      featured: z.boolean().optional(),
      draft: z.boolean().optional(),
      tags: z.array(z.string()).default(["others"]),
      ogImage: image()
        .refine(img => img.width >= 1200 && img.height >= 630, {
          message: "OpenGraph image must be at least 1200 X 630 pixels!",
        })
        .or(z.string())
        .optional(),
      description: z.string(),
      canonicalURL: z.string().optional(),
      readingTime: z.string().optional(),
    }),
});
```

为了防止 IDE 在博客引擎文件中报错，我还做了以下更改：

1. 在 `src/layouts/Layout.astro` 的第 15 行添加了 `| null`，使其看起来像这样：

```typescript
export interface Props {
  title?: string;
  author?: string;
  description?: string;
  ogImage?: string;
  canonicalURL?: string;
  pubDatetime?: Date;
  modDatetime?: Date | null;
}
```

2. 在 `src/components/Datetime.tsx` 的第 5 行添加了 `| null`...
