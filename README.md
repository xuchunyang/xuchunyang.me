# xuchunyang.me

徐春阳（xuchunyang）的个人站点。Astro + Cloudflare Pages。

## 开发

```sh
npm install
npm run dev       # http://localhost:4321
npm run build     # 产物在 dist/
npm run preview
```

## 写博客

在 `src/content/blog/` 下新增 `.md` 文件，frontmatter：

```yaml
---
title: "标题"
description: "简介（可选）"
pubDate: 2026-04-23
tags: ["linux", "pi"]   # 可选
draft: false            # 可选，true 则不发布
---
```

文件名 `foo.md` 对应 URL `/blog/foo/`。

## 部署到 Cloudflare Pages

1. 推送仓库到 GitHub（例如 `github.com/xuchunyang/xuchunyang.me`）。
2. Cloudflare Dashboard → Workers & Pages → Create → Pages → Connect to Git → 选仓库。
3. 构建设置：
   - Framework preset: **Astro**
   - Build command: `npm run build`
   - Build output directory: `dist`
   - 环境变量：`NODE_VERSION=20`
4. 绑定自定义域名：Pages 项目 → Custom domains → 添加 `xuchunyang.me` 和 `www.xuchunyang.me`。
   如果域名 DNS 已经托管在 Cloudflare，会自动写入 CNAME。

纯静态站点，无需 Workers / Functions / SSR adapter。

## 结构

```
src/
├── content/blog/          # 博文 markdown
├── content.config.ts      # blog collection schema
├── layouts/Base.astro
├── components/{Header,Footer,PostList}.astro
├── pages/
│   ├── index.astro        # 首页
│   ├── about.astro
│   ├── blog/
│   │   ├── index.astro
│   │   └── [...slug].astro
│   └── rss.xml.js
└── styles/global.css
```
