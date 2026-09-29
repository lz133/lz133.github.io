# lz133's Hexo Blog

这个仓库使用两个分支管理博客：

- `source`：保存 Hexo 源码、文章、主题配置和依赖锁文件。迁移或换电脑时克隆这个分支。
- `main`：保存 `hexo generate` 生成的静态网站，由 GitHub Pages 发布，不需要手动编辑。

## 环境要求

- Node.js 20
- pnpm 10

## 克隆与本地运行

```powershell
git clone -b source https://github.com/lz133/lz133.github.io.git myblog
cd myblog
pnpm install
pnpm server
```

本地预览地址为 <http://localhost:4000>。

## 新建与发布文章

```powershell
pnpm exec hexo new "文章标题"
pnpm server
pnpm run clean
pnpm run build
pnpm run deploy
```

`pnpm run deploy` 会读取当前 `public` 目录，并把生成后的网站推送到同一仓库的 `main` 分支。

## 主题配置

NexT 通过 pnpm 安装，主题文件位于 `node_modules/hexo-theme-next`。站点覆盖配置位于根目录的 `_config.next.yml`：

- 不要直接修改 `node_modules/hexo-theme-next/_config.yml`。
- 主题设置统一修改 `_config.next.yml`。
- 文章位于 `source/_posts`。
- 分类和标签入口页位于 `source/categories/index.md` 与 `source/tags/index.md`。

## 保存源码修改

```powershell
git status
git add .
git commit -m "描述本次修改"
git push
```

`node_modules`、`public`、`db.json` 和 Hexo 的临时部署目录都已经排除，不会提交到源码分支。
