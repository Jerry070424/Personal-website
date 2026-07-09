# 个人网站学习指南

如果你是编程新手，这份文档从头解释这个网站"用了什么"以及"怎么维护它"。

---

## 一、整体概念：你的网站是怎么工作的？

你的网站本质上是一组 **HTML 文件**（就是浏览器能识别的网页文件）。

传统做法是你手动写每个页面的 HTML。但这个网站用了**框架**来自动生成 HTML，你只需要写**内容和配置**，框架帮你组装成完整的网页。

比喻：
- **你写**：一篇博客文章（纯文字）
- **Astro（框架）**帮你：把这篇文章装进漂亮的页面模板，生成完整的 HTML
- **Tailwind（样式工具）**负责：让页面看起来好看——颜色、间距、字体
- **最终用户看到**：一个完整的漂亮网页

---

## 二、技术栈详解

### 2.1 Astro（核心框架）

**是什么**：一个"静态站点生成器"。它的工作是把你的内容和模板合并，生成最终的 HTML 文件。

**你不需要学**：Astro 的复杂配置。你只需要知道三个概念：

#### 页面（Pages）
`src/pages/` 目录下的每个文件对应网站的一个页面：
- `index.astro` → 首页（`/`）
- `about.astro` → 关于页（`/about`）
- `blog/index.astro` → 博客列表页（`/blog`）

#### 布局（Layouts）
`src/layouts/BaseLayout.astro` 是**所有页面的外壳**，包含：
- 顶部的导航栏
- 底部的页脚
- HTML 头部（标题、描述、字体加载）

所有页面都套用这个外壳，所以你只需要改一个文件就能改变全站的外观。

#### 组件（Components）
`src/components/` 里是可复用的"积木块"。比如 `ScrollReveal.astro` 是一个**滚动动画组件**——把它包在任何内容外面，内容就会在滚动时优雅地出现。

---

### 2.2 Tailwind CSS（样式工具）

**是什么**：一种写 CSS 的方式。传统 CSS 需要你单独写一个样式文件，Tailwind 允许你直接在 HTML 标签上写样式类名。

**例子**：
```html
<!-- 不用 Tailwind 的写法 -->
<div class="my-box">你好</div>
<!-- 需要额外写：.my-box { color: blue; font-size: 24px; } -->

<!-- 用 Tailwind 的写法 -->
<div class="text-blue-500 text-2xl">你好</div>
<!-- 类名本身就是样式，不需要额外写 CSS -->
```

**你只需要知道**：
- `text-lg` = 大号文字
- `text-gray-400` = 灰色文字
- `mb-4` = 下边距 4 个单位
- `bg-dark-800` = 深色背景
- `rounded-xl` = 大圆角
- `p-6` = 内边距 6 个单位
- `flex` / `grid` = 布局模式
- `hover:` 开头 = 鼠标悬停时的样式

**设计令牌（就是颜色系统）** 定义在 `src/styles/global.css` 中：
- `--color-accent-cyan: #22d3ee` → 青色强调色
- `--color-accent-purple: #a78bfa` → 紫色强调色
- `--color-dark-900: #0a0a0f` → 最深背景色

在网页上用 `text-accent-cyan`、`bg-dark-900` 就能使用这些颜色。

---

### 2.3 MDX（内容格式）

**是什么**：一种在 Markdown（简易标记语言）中可以嵌入组件的格式。

**你实际需要做的**：只用 Markdown 语法写文章就行。

**Markdown 基础语法**：
```markdown
# 一级标题
## 二级标题

**加粗文字**
*斜体文字*

- 列表项1
- 列表项2

[链接文字](https://链接地址)

`代码片段`
```

**每篇博客/项目的头部**（frontmatter，用 `---` 包裹）：
```yaml
---
title: "文章标题"           # 标题
description: "简介"         # 摘要
pubDate: 2025-09-01        # 发布日期
tags: ["标签1", "标签2"]   # 标签
---
```

---

## 三、你怎么维护这个网站

### 3.1 改个人信息

编辑 `src/config/site.ts`，这个文件集中管理所有个人信息：

```typescript
export const siteConfig = {
  title: "你的名字 | Personal Site",  // 浏览器标签栏显示的标题
  description: "一句话描述你自己",
  author: {
    name: "你的名字",            // 首页显示的名字
    email: "你的邮箱",           // 联系邮箱
    bio: "南京大学 · 软件工程 & 经济学 双学位在读",  // 个人简介
  },
  social: [
    { name: "GitHub", url: "https://github.com/你的用户名" },
  ],
  nav: [
    // 导航栏菜单项
    { label: "首页", href: "/" },
    { label: "博客", href: "/blog" },
    { label: "项目", href: "/projects" },
    { label: "关于", href: "/about" },
  ],
};
```

改完后，所有引用这些信息的地方（导航栏、首页、关于页）都会自动更新。

### 3.2 写一篇博客

1. 在 `src/content/blog/` 目录下新建一个 `.mdx` 文件
2. 文件名就是网址（例如 `my-first-post.mdx` → 访问 `/blog/my-first-post`）

文件内容模板：

```mdx
---
title: "我的第一篇博客"
description: "这是博客的简短描述，会显示在博客列表页。"
pubDate: 2025-09-15
tags: ["学习", "随笔"]
---

这里是正文。

你可以用 **Markdown** 语法写文章。

- 列表
- 列表

## 二级标题

> 引用文字

`代码` 等等。
```

写完保存，刷新网页就能看到。

### 3.3 添加一个项目

和博客类似，在 `src/content/projects/` 下新建 `.mdx` 文件：

```mdx
---
title: "我的项目"
description: "项目简介"
pubDate: 2025-09-15
tags: ["Astro", "TypeScript", "Python"]
---

这里写项目的详细说明、技术方案、成果等。
```

### 3.4 修改首页文案

首页内容在 `src/pages/index.astro`，找到对应的文字直接改：

- **Hero 区**（大标题下面的描述文字）
- **关于我段落**（section 注释为 "Quick About" 的部分）
- **联系邮箱**

### 3.5 改颜色或样式

所有颜色定义集中在 `src/styles/global.css` 的 `@theme` 块中：

```css
@theme {
  --color-accent-cyan: #22d3ee;      /* 青色 — 主色调 */
  --color-accent-purple: #a78bfa;    /* 紫色 — 辅色调 */
  --color-dark-900: #0a0a0f;         /* 最深背景 */
  --color-dark-800: #12121a;         /* 次深背景（卡片） */
}
```

想换颜色，只改这些值就行。比如想把青色换成橙色，改成 `--color-accent-cyan: #fb923c;`。

---

## 四、本地预览

开发时预览修改效果：

```bash
npm run dev
```

终端会显示一个地址（通常是 `http://localhost:4321`），在浏览器打开就能看到网站。

修改任何文件后，浏览器会自动刷新，不需要手动操作。

---

## 五、你应该先学什么（学习路线推荐）

作为大一双学位学生，如果你以后想真正理解并能自由修改这个网站，建议按顺序学：

### 第一阶段（基础，1-2 周）
1. **HTML 基础** — 了解标签、属性、DOM 结构
   - 推荐：MDN Web Docs 的 HTML 教程
2. **CSS 基础** — 选择器、盒模型、Flexbox、Grid
   - 推荐：Flexbox Froggy 游戏入门
3. **Markdown 语法** — 写博客文章必备
   - 30 分钟就能学会

学完这阶段，你就能自由编辑网站的文字内容、文章、项目信息。

### 第二阶段（进阶级，2-4 周）
4. **Tailwind CSS** — 理解类名系统，能自己调整样式
5. **JavaScript 基础** — 变量、函数、事件
6. **Astro 基础** — 了解 `.astro` 文件语法

学完这阶段，你能修改网站布局、添加新页面、自定义样式。

### 第三阶段（开发者级，1-2 个月）
7. **TypeScript** — 了解类型系统
8. **Git 版本控制** — 管理代码版本
9. **React**（可选）— 如果你想写交互性更强的组件

---

## 六、常见问题

### Q: 网站做好了，怎么让别人访问？
A: 以后会配置 GitHub + Vercel 自动部署，你把代码推送到 GitHub，Vercel 自动上线。

### Q: 我可以自己加新页面吗？
A: 可以。在 `src/pages/` 下新建 `.astro` 文件，比如新建 `src/pages/reading.astro`，访问 `/reading` 就能看到。

### Q: 我想换个字体？
A: 改两个地方：
1. `src/layouts/BaseLayout.astro` — 替换 Google Fonts 的链接
2. `src/styles/global.css` — 修改 `--font-sans` 的值

### Q: 我改乱了怎么办？
A: 只要不删 `node_modules/` 和 `dist/` 目录，都可以通过重新安装修复。以后配了 Git 就更安全，可以回退到之前的版本。
