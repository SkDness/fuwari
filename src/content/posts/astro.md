---
title: 使用Fuwaru主题部署Astro博客
published: 2026-06-09
description: Astro博客搭建，并使用Fuwari主题
tags: [博客]
category: 教程
draft: false
---

# 使用Fuwaru主题部署Astro博客



> 直接复制就能用的完整配置方案，按步骤填就行，在 Cloudflare Pages 测试部署成功。

---

## 1. 基础配置（直接照着填）

| 配置项 | 填写内容 | 说明 |
|--------|----------|------|
| 生产分支 | `main` | 优先推荐，按需调整 |
| 框架预设 | `Astro` | 直接选 Astro |
| 构建输出目录 | `dist` | Astro 默认输出目录 |

---


## 2.用 pnpm（推荐，和 Fuwari 官方一致，构建更快）

#### 第一步：构建命令填

```bash
npx pnpm install --frozen-lockfile && pnpm run build
```

#### 第二步：添加 2 个环境变量

在「环境变量（高级）」里添加：

| 变量名 | 值 | 作用 |
|--------|----|------|
| `NODE_VERSION` | `20` | 指定 Node.js 版本，兼容最新 Astro |
| `ENABLE_PNPM` | `true` | Cloudflare 自动安装 pnpm |

✅ **优点**：依赖安装更快，和 Fuwari 官方开发环境一致，减少兼容性问题。

---

## 3. 其他高级配置（一般不用改）

- **根目录（高级）**：保持空值，除非你的项目文件在仓库的子文件夹里（比如 `/blog/`）
- **其他环境变量**：如果你的博客需要 API、评论、分析等额外配置，后续再添加，首次部署先不填。

---

## 4. 部署操作步骤

1. 把上面的配置填好
2. 点击右下角「保存并部署」
3. 等待 Cloudflare 构建（一般 1~3 分钟）
4. 构建完成后，会给你一个默认的 `*.pages.dev` 域名，直接就能访问博客了。

---

## 5. 构建失败应急方案

如果构建报错，可以试试下面这个通用修复版命令：

```bash
npm install --force && npm run build
```

> 这个命令会强制重新安装依赖，解决大部分依赖版本冲突问题。
