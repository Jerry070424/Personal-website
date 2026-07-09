# 个人网站开发记录 (v2)

> 最后更新: 2026-04-28

## 项目状态

✅ 基础搭建完成
✅ 页面构建完成
✅ 动效增强完成
⏸️ 部署到 Vercel — **未完成，暂停在第一步**

---

## 当前进度

### 已完成

1. **项目初始化** — Astro 5 + Tailwind CSS v4 + MDX 手动搭建，无脚手架
2. **设计系统** — 深色主题（#0a0a0f 背景），cyan→purple 渐变主色调，Inter + Noto Sans SC 字体
3. **布局** — BaseLayout（导航栏 + 页脚 + SEO head），导航栏滚动隐藏/显示
4. **首页 5 个区块** — Hero（Canvas 粒子网络背景 + 渐变动画标题）、关于我、项目精选（3D 倾斜卡片）、最新博客（左侧渐变色条 hover 效果）、联系方式（发光按钮）
5. **博客系统** — MDX 内容集合，列表页按日期排序，文章详情页
6. **项目展示** — 列表页 + 详情页，支持标签
7. **关于页** — 个人信息 + 经历时间线
8. **动效** — 粒子网络 Canvas、ScrollReveal 入场动画、3D TiltCard、View Transitions 页面过渡、导航栏滚动隐藏、卡片悬停发光
9. **SEO** — Sitemap 自动生成

### 未完成（暂停点）

**部署到 Vercel（暂停在第 1 步）：**

- [ ] 在 GitHub 上创建仓库 `https://github.com/new`
- [ ] 本地提交代码并推送到 GitHub
- [ ] 打开 vercel.com，用 GitHub 账号登录
- [ ] 点击 "Add New → Project"，导入 `personal-website` 仓库
- [ ] Vercel 自动检测 Astro 项目，保持默认设置，点击 "Deploy"
- [ ] 部署完成，获得 `xxx.vercel.app` 免费域名

### 后续可做

- [ ] 购买自定义域名（推荐 Cloudflare 或 Namecheap）
- [ ] 升级 Astro v6
- [ ] RSS feed
- [ ] 标签聚合页
- [ ] 暗色/亮色模式切换
- [ ] 文章搜索功能

---

## 技术栈速览

| 技术 | 作用 | 学习难度 |
|---|---|---|
| Astro | 框架，把内容和模板组装成网页 | ★☆☆ |
| Tailwind CSS | 样式，在 HTML 上写类名控制外观 | ★☆☆ |
| MDX / Markdown | 内容格式，写博客和项目介绍 | ★☆☆ |
| TypeScript | 配置文件的类型系统 | ★★☆ |

学习路线建议：先学 HTML + CSS + Markdown（1-2 周），再学 Tailwind + Astro（2-4 周），最后学 Git + TypeScript（1-2 月）。

详见 `docs/learning-guide.md`。

---

## 项目结构

```
D:\Personal-website\
├── src/
│   ├── components/
│   │   ├── ParticleBackground.astro   # Hero 粒子网络 Canvas
│   │   ├── ScrollReveal.astro         # 滚动入场动画
│   │   └── TiltCard.astro             # 3D 悬停倾斜卡片
│   ├── config/
│   │   └── site.ts                    # ★ 改个人信息在这里
│   ├── content/
│   │   ├── config.ts                  # 内容类型定义
│   │   ├── blog/                      # ★ 写博客在这里
│   │   └── projects/                  # ★ 加项目在这里
│   ├── layouts/
│   │   └── BaseLayout.astro           # 全站外壳（导航栏 + 页脚）
│   ├── pages/
│   │   ├── index.astro                # 首页
│   │   ├── about.astro                # 关于我
│   │   ├── blog/index.astro           # 博客列表
│   │   ├── blog/[slug].astro          # 博客文章
│   │   ├── projects/index.astro       # 项目列表
│   │   └── projects/[slug].astro      # 项目详情
│   └── styles/
│       └── global.css                 # ★ 改颜色在这里
├── public/favicon.svg
├── docs/
│   ├── dev-log.md                     # 开发笔记
│   └── learning-guide.md              # 学习指南
├── astro.config.mjs
├── tsconfig.json
└── package.json
```

## 常用命令

```bash
npm run dev       # 启动开发服务器 → http://localhost:4321
npm run build     # 构建项目到 dist/
npm run preview   # 预览构建结果
```

---

## 对话记录要点

- 用户是南京大学大一学生，SE + 经济学双学位，编程基础薄弱
- 想要综合性个人网站（简历 + 博客 + 项目），炫酷风格
- 技术选型：Astro + Tailwind CSS v4 + MDX，静态站点生成器
- 已讲解 npm run dev 含义、技术栈概念、域名是什么
- 已创建学习指南 docs/learning-guide.md
- 部署暂停原因：用户当时没继续

### 下次继续时恢复上下文

1. dev server 如果没在运行，先 `npm run dev`
2. 确认配置文件 `src/config/site.ts` 中的个人信息已更新
3. 如要继续部署：先让用户在 GitHub 创建仓库，然后推送代码，最后在 Vercel 导入
