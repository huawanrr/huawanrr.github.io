# huawan 的技术笔记

博客：**https://huawanrr.github.io/zh/**

使用 Hugo + PaperMod + GitHub Pages。推送到 `main` 后，GitHub Actions 自动构建并发布。

外观采用简洁的英伦书刊风格：暖白纸色、衬线标题、细线分隔和少量酒红点缀。默认浅色，可手动切换深色。

## 直接在 GitHub 发文章

1. 打开仓库 `content/posts` 目录，选择 **Add file → Create new file**。
2. 文件名填写 `my-first-post/index.md`（每篇文章一个独立目录）。
3. 填入下面的内容，修改标题、日期、标签和正文。
4. 点击 **Commit changes**，等待 Actions 显示绿色。通常几分钟后博客就会更新。

```markdown
---
title: "我的第一篇技术笔记"
date: 2026-10-19T17:00:00+08:00
draft: false
description: "一句话概括这篇文章。"
tags: ["Python", "学习笔记"]
categories: ["编程"]
---

## 要解决的问题

写下你的问题。

## 思路与实践

写下分析、代码和实验过程。

## 结果与复盘

写下结果、结论和未验证的部分。
```

**注意：** 日期填写实际发布日期，未来日期的文章默认不会发布；`draft: true` 的文章也不会发布。文件夹名使用英文、数字和短横线，发布后尽量保持不变。

### 放图片

把图片上传到文章所在目录，例如 `content/posts/my-first-post/figure.png`，正文写 `![图片说明](figure.png)`。

### 修改已有文章

打开文章的 `index.md`，点击铅笔图标编辑并提交即可。标签、归档、搜索和 RSS 都会自动更新。

## 修改博客资料

| 要修改的内容 | 文件 |
| --- | --- |
| 站名、首页介绍、菜单、GitHub 链接 | `hugo.yaml` |
| 关于我 | `content/about.md` |
| 文章 | `content/posts/` |
| 字体、间距等样式 | `assets/css/extended/custom.css` |
| 书刊报头、导航和主题切换按钮 | `layouts/_partials/header.html` |
| 自动部署 | `.github/workflows/hugo.yaml` |

## 本地预览

安装 [Hugo](https://gohugo.io/installation/)（工作流固定使用 0.168.0）。

```bash
git clone --recurse-submodules https://github.com/huawanrr/huawanrr.github.io.git
cd huawanrr.github.io
hugo server -D
```

打开终端显示的地址。本地 `-D` 模式会显示草稿，线上不会。

新建草稿：

```bash
hugo new content posts/my-new-post/index.md
```

发布前改成 `draft: false`，然后提交并推送。

```bash
git add .
git commit -m "Add a new post"
git push
```

只构建：`hugo --gc --minify`，生成目录是 `public/`，不需要提交。

## 部署设置

GitHub 仓库 **Settings → Pages → Build and deployment → Source** 选择 **GitHub Actions**。

如果构建失败，查看仓库的 **Actions** 标签。不要把源码直接当作静态 HTML 发布。

## 主题

[PaperMod](https://github.com/adityatelange/hugo-PaperMod) 通过 Git submodule 固定在一个提交；许可证在 `themes/PaperMod/LICENSE`。初始化时只写入开站文章。

更新主题前先预览检查：`git submodule update --remote themes/PaperMod`。
