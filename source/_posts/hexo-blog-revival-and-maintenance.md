---
title: Hexo 博客重新启用：修复记录与更新维护指南
date: 2026-09-29 10:23:08
categories:
  - 博客维护
tags:
  - Hexo
  - GitHub Pages
  - 维护记录
---

这个博客已经很久没有更新，这次重新整理本地 Hexo 工程、恢复构建与发布流程，并把后续的维护方式记录下来，方便以后直接照着操作。

## 这次修复了什么

本次检查和调整包括：

1. 保留现有 Hexo 源文件、主题和文章，不重建站点。
2. 将 `_config.yml` 中的站点地址从示例地址改为正式地址 `https://lz133.github.io`。
3. 修正 `keywords` 配置的 YAML 写法。
4. 补齐 Hexo 的 Git 部署插件，使 `hexo deploy` 可以将生成后的静态站点发布到 `main` 分支。
5. 执行一次正式构建，确认文章可以正常生成。
6. 增加这篇维护记录，作为以后继续写作和排障的入口。

本站目前使用 Hexo 8、Node.js 20 和 pnpm 10。博客部署地址是：

- 网站：<https://lz133.github.io/>
- 部署仓库：<https://github.com/lz133/lz133.github.io>

## 本地预览

首次恢复项目或拉取源码后，先安装依赖：

```powershell
pnpm install
```

启动本地预览服务：

```powershell
pnpm server
```

浏览器访问 `http://localhost:4000`。预览时可以直接检查文章排版、链接和图片是否正常。

## 发布新文章

创建文章：

```powershell
pnpm exec hexo new "文章标题"
```

文章会生成在 `source/_posts` 目录。编辑完成后，先清理并重新生成静态文件：

```powershell
pnpm run clean
pnpm run build
```

最后发布到 GitHub Pages：

```powershell
pnpm run deploy
```

`pnpm run deploy` 会把 `public` 中生成的静态文件提交到 `lz133/lz133.github.io` 仓库的 `main` 分支。发布完成后，等待 GitHub Pages 更新，再打开 <https://lz133.github.io/> 检查结果。

## 日常维护流程

以后更新博客时，可以固定使用下面的流程：

1. 先执行 `pnpm install`，确保本地依赖完整。
2. 使用 `pnpm exec hexo new "文章标题"` 新建文章。
3. 使用 Markdown 编写内容，需要图片时把图片放在 `source` 下的稳定目录中引用。
4. 使用 `pnpm server` 本地预览。
5. 使用 `pnpm run clean` 和 `pnpm run build` 检查构建结果。
6. 使用 `pnpm run deploy` 发布，然后检查线上页面。
7. 定期执行 `pnpm outdated` 查看依赖更新，并用 Git 保存 Hexo 源文件。

## 发布与备份注意事项

- GitHub 登录凭据应由 Git Credential Manager 或系统凭据管理器保存，不要把个人访问令牌直接写进 `_config.yml`。
- 不要提交 `node_modules`、`public`、`db.json` 和 Hexo 临时部署目录，这些内容已经由 `.gitignore` 排除。
- 当前完整 Hexo 工程保存在 `lz133.github.io` 仓库的 `source` 分支，静态网站保存在 `main` 分支。迁移电脑时克隆 `source` 分支即可恢复文章、配置和依赖锁定信息。
- GitHub Pages 的发布源需要与部署方式保持一致。当前方案直接由本机将静态文件推送到 `lz133.github.io` 的 `main` 分支，不要再同时用另一套自动部署覆盖同一分支。
- 发布前至少检查首页、文章详情、归档、分类、标签和移动端布局。

## 本次结论

博客没有损坏，主要问题是本地工程长期未维护、配置仍保留示例值，并且缺少 Git 部署插件。完成这些修正后，写作、构建和发布流程已经恢复。后续只需要按照“新建文章、本地预览、构建、部署、线上检查”的顺序维护即可。
