---
title: "第一篇：从源码构建这个 Hugo 博客"
date: 2026-07-07T17:30:00+08:00
draft: false
math: false
tags: ["hugo", "github-pages", "source"]
categories: ["建站记录"]
summary: "记录如何从这份源码开始，在本地预览 Hugo 博客，并通过 GitHub Actions 发布到 GitHub Pages。"
---

这篇文章是这个博客重新整理后的第一篇。目标很简单：把“源码如何变成一个可访问的网站”这条链路记录下来，之后迁移、重装或交给另一台机器接手时，不需要再从记忆里拼流程。

## 源码里有什么

当前仓库是一套 Hugo 站点源码：

```text
.
├── hugo.yaml                 # 站点配置
├── content/                  # 页面与文章
│   ├── about.md
│   ├── archives.md
│   ├── search.md
│   └── posts/                # 博客文章
├── layouts/                  # 覆盖主题的局部模板
├── themes/PaperMod/          # PaperMod 主题
└── .github/workflows/hugo.yml# GitHub Pages 自动部署
```

其中最重要的是 `hugo.yaml` 和 `content/posts/`。前者决定站点名称、菜单、主题、搜索和渲染规则；后者放每一篇 Markdown 文章。

## 准备 Hugo

本地只需要安装 Hugo Extended 版本，GitHub Actions 里使用的是 `0.164.0`：

```bash
brew install hugo
hugo version
```

如果环境里没有 Homebrew，也可以直接下载 Hugo Extended 的 release 包。关键点是选择 extended 版本，因为主题和样式构建通常依赖 extended 能力。

## 本地预览

进入源码目录后启动开发服务器：

```bash
hugo server -D
```

然后打开终端里显示的本地地址，一般是：

```text
http://localhost:1313/
```

`-D` 表示草稿文章也一起展示。正式发布时，只有 `draft: false` 的文章会进入线上站点。

## 新建文章

推荐让 Hugo 按模板生成文章：

```bash
hugo new content posts/my-new-post.md
```

生成后重点检查 front matter：

```yaml
---
title: "文章标题"
date: 2026-07-07T18:00:00+08:00
draft: false
tags: ["hugo"]
categories: ["建站记录"]
summary: "一句话摘要"
---
```

写完后本地预览没有问题，就可以提交。

## 发布到 GitHub Pages

这个仓库已经配置了 `.github/workflows/hugo.yml`。每次 push 到 `main`，GitHub Actions 会自动：

1. 安装 Hugo Extended；
2. checkout 源码；
3. 执行 `hugo --gc --minify` 构建；
4. 把 `public/` 发布到 GitHub Pages。

日常更新只需要：

```bash
git add content/posts/my-new-post.md
git commit -m "post: my new post"
git push origin main
```

几分钟后访问 `https://tanmo-ai.github.io/`，新文章就会出现在首页和文章列表里。

## 这次重新开始

这次整理顺手清掉了旧文章和旧提交记录，让仓库从一个干净的初始提交重新开始。以后这里会只保留真正想长期维护的内容，博客本身也尽量保持简单：Markdown 写作，Git 管理，GitHub Actions 发布。
