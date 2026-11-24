---
title: 用 Hexo + Butterfly + Vercel 搭建个人博客
date: 2026-11-24 11:00:00
tags:
  - Hexo
  - Vercel
  - 教程
categories:
  - 技术
---

记录一下这套博客方案的完整搭建过程，方便以后重装或者安利给朋友。

<!-- more -->

## 为什么选这套组合

| 方案 | 优点 | 缺点 |
| --- | --- | --- |
| Hexo + Butterfly | 生态成熟、主题漂亮、构建快 | 需要自己维护依赖 |
| WordPress | 插件丰富 | 需要服务器和数据库 |
| Hugo | 构建极快 | 主题风格偏好因人而异 |

静态站点没有数据库和服务器成本，托管在 Vercel 上，配合 GitHub 自动部署，基本是零运维。

## 本地写作流程

新建文章：

```bash
npx hexo new "文章标题"
```

本地预览：

```bash
npx hexo server
```

打开 `http://localhost:4000` 即可看到效果。

## 部署到 Vercel

在 Vercel 中导入 GitHub 仓库，构建设置保持默认即可：

- **Build Command**：`npm run build`（即 `hexo generate`）
- **Output Directory**：`public`
- **Install Command**：`npm install`

然后在项目的 Domains 里绑定 `prz.best`，按提示配置 DNS 记录即可。

之后每次 `git push`，Vercel 都会自动重新构建并发布，写作只需要专注 Markdown 本身。

## 常用插件

```yaml
# _config.yml 中的主题
theme: butterfly
```

- `hexo-generator-searchdb`：本地搜索
- `hexo-wordcount`：字数统计
- `hexo-generator-sitemap` / `hexo-generator-feed`：SEO 与 RSS

主题的个性化配置都放在根目录的 `_config.butterfly.yml` 里，升级主题时不会覆盖你的修改。
