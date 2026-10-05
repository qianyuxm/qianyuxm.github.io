# qianyuxm 的 Hexo 博客

这是部署在 <https://qianyuxm.github.io> 的个人博客，使用 [Hexo](https://hexo.io/zh-cn/) 和现代卡片式的 [Butterfly](https://butterfly.js.org/) 主题。

## 环境要求

- Node.js 20.19.0 或更高版本（推荐使用 Node.js 24 LTS）
- npm

首次使用时安装依赖：

```bash
npm ci
```

## 本地开发

启动本地预览服务器：

```bash
npm run server
```

默认访问地址为 <http://localhost:4000>。修改 `_config.yml` 可调整站点名称、作者、描述和文章链接等 Hexo 基本信息；修改 `_config.butterfly.yml` 可调整导航、卡片、代码块、深色模式和本地搜索等主题选项。

站内搜索使用构建时生成的本地索引，不需要 Algolia 等外部私密服务。导航中的标签、分类和关于页面分别位于 `source/tags/index.md`、`source/categories/index.md` 和 `source/about/index.md`。

## 写文章

创建一篇新文章：

```bash
npm run new -- "文章标题"
```

文章会生成到 `source/_posts/`。编辑 Markdown 文件顶部的 `title`、`date`、`categories` 和 `tags` 后即可开始写作。

例如：

```yaml
---
title: 文章标题
date: 2026-09-19 20:00:00
categories:
  - 技术
tags:
  - Hexo
---
```

## 构建

生成静态网站：

```bash
npm run build
```

生成结果位于 `public/`。如需清理缓存和生成文件，可运行：

```bash
npm run clean
```

提交前可执行完整的最小检查：

```bash
npm test
```

## 部署到 GitHub Pages

仓库中的 `.github/workflows/pages.yml` 会在推送到 `master` 分支后自动执行以下步骤：

1. 使用 `npm ci` 安装锁定版本的依赖。
2. 使用 `npx hexo generate` 构建网站。
3. 上传 `public/` 并部署到 GitHub Pages。

首次部署前，需要在 GitHub 仓库中打开 **Settings → Pages**，将 **Build and deployment → Source** 设置为 **GitHub Actions**。之后推送到 `master`，或在 **Actions** 页面手动运行 `Deploy Hexo site to Pages` 工作流即可部署。

根目录中原有的 `index.html` 被保留，但 GitHub Actions 部署的是 `public/` artifact，因此不会使用该文件作为线上首页。
