# Tanmo 的知识花园

这是一个基于 Hugo + PaperMod + GitHub Pages 的个人博客源码仓库。

线上地址：[https://tanmo-ai.github.io/](https://tanmo-ai.github.io/)

## 目录结构

```text
.
├── hugo.yaml                  # Hugo 站点配置
├── archetypes/                # 新文章模板
├── content/                   # 页面与文章
│   ├── about.md
│   ├── archives.md
│   ├── search.md
│   └── posts/                 # 博客文章
├── layouts/                   # 自定义模板覆盖
├── themes/PaperMod/           # PaperMod 主题
└── .github/workflows/hugo.yml # GitHub Pages 自动部署
```

## 本地构建

安装 Hugo Extended。GitHub Actions 当前使用 `0.164.0`：

```bash
brew install hugo
hugo version
```

启动本地预览：

```bash
hugo server -D
```

生成静态站点：

```bash
hugo --gc --minify
```

构建产物会输出到 `public/`，该目录不需要提交。

## 写新文章

使用 Hugo 模板创建文章：

```bash
hugo new content posts/my-topic.md
```

写完后把 front matter 里的 `draft` 改成 `false`：

```yaml
---
title: "文章标题"
date: 2026-07-07T18:00:00+08:00
draft: false
math: false
tags: ["hugo"]
categories: ["建站记录"]
summary: "一句话摘要"
---
```

## 发布

仓库已经配置 GitHub Actions。push 到 `main` 后，会自动构建并发布到 GitHub Pages。

```bash
git add .
git commit -m "post: my topic"
git push origin main
```

部署完成后访问：

```text
https://tanmo-ai.github.io/
```

## 重新初始化记录

这个仓库已经清理旧文章与旧提交历史，从一个新的初始化提交重新开始。后续内容会以 Markdown 源码为准，通过 GitHub Actions 自动发布。
