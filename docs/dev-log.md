# 个人网站开发记录

## 项目背景

南京大学大一学生，软件工程与经济学双学位。用 Claude Code 搭建个人网站，用于展示个人信息、项目经历和博客内容。

## 技术选型

| 层 | 选择 | 理由 |
|---|---|---|
| 框架 | **Astro 5.18** | 内容型网站最优选，零 JS 开销，MDX 支持成熟 |
| 样式 | **Tailwind CSS 4.2** | 原子化 CSS，v4 的 `@theme` 指令自定义设计令牌 |
| 内容 | **MDX** | 在 Markdown 中嵌入组件，灵活扩展 |
| 部署 | **Vercel**（待配置） | 免费，自动 CI/CD |

## 设计系统

### 颜色
- 背景：`#0a0a0f`（深色）到 `#1a1a26`
- 强调色：cyan `#22d3ee` → purple `#a78bfa`（渐变为视觉主调）
- 文字：`#e2e8f0`（主）、`#9ca3af`（次要）
- 装饰：高斯模糊光晕（`blur-3xl` + 半透明色块）

### 字体
- 英文字体：Inter
- 中文字体：Noto Sans SC
- 等宽字体：JetBrains Mono
- 通过 Google Fonts CDN 加载

### 动效
- **gradient 动画**：Hero 标题渐变背景慢速移动，`background-size: 200%` + `@keyframes gradient`
- **ScrollReveal**：IntersectionObserver 驱动的 fade-up 入场动画，每区块延迟递增
- **光晕脉冲**：背景光晕球体 CSS `animate-pulse`
- **hover 效果**：卡片上移 + 边框变色 + 下划线展开

## 项目结构

```
D:\Personal-website\
├── src/
│   ├── components/
│   │   └── ScrollReveal.astro      # 滚动入场动画组件
│   ├── config/
│   │   └── site.ts                 # 站点配置（改这里填个人信息）
│   ├── content/
│   │   ├── config.ts               # 内容类型定义
│   │   ├── blog/                   # 博客 MDX 文件
│   │   └── projects/               # 项目 MDX 文件
│   ├── layouts/
│   │   └── BaseLayout.astro        # 全局布局（导航栏 + 页脚 + SEO head）
│   ├── pages/
│   │   ├── index.astro             # 首页
│   │   ├── about.astro             # 关于我
│   │   ├── blog/
│   │   │   ├── index.astro         # 博客列表
│   │   │   └── [slug].astro        # 博客文章页
│   │   └── projects/
│   │       ├── index.astro         # 项目列表
│   │       └── [slug].astro        # 项目详情页
│   └── styles/
│       └── global.css              # 全局样式 + Tailwind 主题定义
├── public/
│   └── favicon.svg                 # 渐变图标
├── astro.config.mjs
├── tsconfig.json
└── package.json
```

## 页面路由

| 路由 | 内容 | 状态 |
|---|---|---|
| `/` | 首页（Hero + About + Projects + Blog + Contact） | ✅ |
| `/about` | 个人信息 + 时间线 | ✅ |
| `/blog` | 博客列表，按日期排序 | ✅ |
| `/blog/:slug` | 博文详情，MDX 渲染 | ✅ |
| `/projects` | 项目列表 | ✅ |
| `/projects/:slug` | 项目详情 | ✅ |

## 开发命令

```bash
npm run dev       # 启动开发服务器 http://localhost:4321
npm run build     # 构建到 dist/
npm run preview   # 预览构建产物
```

## 待做事项

### 内容填充
- [ ] `src/config/site.ts` — 修改姓名、邮箱、GitHub、个人简介
- [ ] `src/pages/index.astro` — 替换 "Your Name"，更新个人简介文案
- [ ] 头像图片放到 `public/avatar.jpg`
- [ ] 在 `src/content/blog/` 下新建 `.mdx` 文件写博客
- [ ] 在 `src/content/projects/` 下新建 `.mdx` 文件加项目

### 后续开发
- [ ] 粒子背景 Hero（Canvas 粒子系统）
- [ ] View Transitions 页面切换动画
- [ ] 暗色/亮色模式切换
- [ ] RSS feed
- [ ] 标签聚合页（按标签筛选博客）
- [ ] ~~升级 Astro v6~~（暂时不建议，v5 稳定够用）

### 部署
- [ ] Git 初始化 + GitHub 仓库
- [ ] Vercel 关联自动部署
- [ ] 自定义域名（可选）

## 开发笔记（搭建过程）
- 2025-09-01：项目初始化，Astro + Tailwind CSS v4 + MDX 配置完成
- 2025-09-01：BaseLayout、导航栏、页脚创建
- 2025-09-01：首页 Hero（渐变光晕 + gradient 动画 + CTA）
- 2025-09-01：ScrollReveal 滚动入场动画组件
- 2025-09-01：博客系统（列表 + 详情页，MDX 内容集合）
- 2025-09-01：项目展示页（列表 + 详情页）
- 2025-09-01：关于我页面（个人信息 + 时间线）
- 2025-09-01：Sitemap 自动生成，SEO 基础优化

## 遇到过的坑
- `create-astro` 脚手架因 GitHub 网络超时无法使用，改为手动搭建
- Tailwind CSS v4 通过 `@tailwindcss/vite` 插件集成到 Astro 的 `vite.plugins`，不需要 `@astrojs/tailwind`
- Tailwind v4 用 `@theme` 指令自定义设计令牌，不是 `tailwind.config.ts`
- Astro 静态模式下内容集合自动生成路由，`getStaticPaths()` 返回 slug 映射
