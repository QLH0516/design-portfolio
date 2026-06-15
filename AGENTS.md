# Studio Namma 网站项目 AI 协作指南 (AGENTS.md)

---

## 项目概述

- **项目**: Studio Namma 品牌网站（仿 studionamma.com 风格）
- **风格**: 极简主义、叙事驱动、高对比黑白 + 强调色
- **目标**: 构建一个高性能、视觉沉浸式的创意工作室展示网站

---

## 角色定义

本项目遵循 AI 辅助开发工作流，请 AI 代理根据自身能力承担以下角色之一：

| 角色 | 职责 |
|------|------|
| **架构师** | 制定技术方案、组件拆分、数据流设计 |
| **设计实现者** | 将 design.md 中的视觉规范转换为 CSS/Tailwind 代码 |
| **交互动效师** | 实现 GSAP/Lenis 动效、滚动动画、过渡效果 |
| **内容整合者** | 对接 CMS/数据源，填充真实内容 |
| **性能优化者** | Lighthouse 评分优化、图片压缩、代码分割 |
| **质量保证者** | 可访问性检查、跨浏览器测试、响应式验证 |

> 同一次会话中，AI 代理可同时承担多个角色，但需明确当前操作属于哪个角色范畴。

---

## 编码规范

### 通用原则

- **语言**: 文件注释、变量命名、提交信息等均使用 **中文**
- **代码风格**: 遵循项目已有风格；新增功能应与原有代码保持视觉与逻辑一致性
- **性能优先**: 图片懒加载、代码分割、字体子集化是必须项
- **避免冗余**: 不要添加不必要的依赖、注释或装饰性代码
- **移动优先响应式**: 所有组件必须先考虑移动端，再扩展到桌面端
- **组件粒度**: 一个文件一个组件，组件文件与导出名称一致（PascalCase）
- **类型先行**: 任何新组件必须先定义接口/类型，再实现逻辑

### HTML / JSX

- 使用语义化 HTML5 标签（section, article, nav, figure, blockquote 等）
- JSX 属性按字母排序，保持一致性
- 图片必须包含 alt 属性，装饰性图片 alt="" 
- 外部链接添加 rel="noopener noreferrer"
- 按钮使用 button 标签而非 div/span（可访问性）
- 避免 div 层级过深（最多不超过 5 层嵌套）

### CSS / 样式

- 使用 **Tailwind CSS** 或 **CSS Modules**（根据项目配置决定）
- 颜色使用 CSS 自定义属性（--color-*），方便主题切换
- 动效缓动函数统一使用 cubic-bezier() 定义在全局变量中
- 禁用 !important — 通过选择器优先级管理样式
- 字体大小使用 rem 或 clamp() 实现流畅缩放
- Tailwind 类名优先顺序：布局 > 间距 > 排版 > 颜色 > 动效
- 自定义样式中尽可能使用 CSS 逻辑属性（margin-inline 替代 margin-left 等）

### JavaScript / TypeScript

- 优先使用 TypeScript，为所有 props 和 state 定义接口
- 避免使用 any，优先使用工具类型（Pick, Omit, Partial, Record）
- 组件使用函数式组件 + Hooks
- 动效逻辑提取到自定义 Hook（如 useScrollReveal, useParallax, useLenis）
- 事件处理函数使用 useCallback 优化性能
- 业务逻辑与 UI 组件分离：数据获取/状态管理放在 lib/ 或 hooks/ 中
- 使用 React.lazy + Suspense 实现代码分割

### 命名规范

| 类型 | 规范 | 示例 |
|------|------|------|
| 组件 | PascalCase | HeroSection.tsx |
| Hooks | use 前缀 + camelCase | useScrollReveal.ts |
| 工具函数 | camelCase | formatDate.ts |
| 类型/接口 | PascalCase + Props/Type | HeroSectionProps |
| 样式文件 | 组件同名 + .module.css | HeroSection.module.css |
| 常量 | UPPER_SNAKE_CASE | SITE_CONFIG.ts |
| 数据文件 | camelCase | projectList.ts |

### Git 提交规范

提交信息格式：[类型]: 中文描述

| 类型 | 使用场景 |
|------|----------|
| feat | 新功能 |
| fix | 修复 bug |
| style | 样式调整（无逻辑变更） |
| refactor | 代码重构 |
| perf | 性能优化 |
| docs | 文档变更 |
| chore | 构建/工具链 |

示例：feat: 添加首页英雄区视差滚动效果

---

## 项目结构

project/
├── public/
│   ├── fonts/          # 自托管字体文件（WOFF2）
│   ├── images/         # 静态图片资源
│   └── favicon.ico
├── src/
│   ├── app/            # Next.js App Router 页面
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   ├── work/
│   │   ├── about/
│   │   └── contact/
│   ├── components/     # 可复用 UI 组件
│   │   ├── layout/     # Header, Footer, Navigation, FullscreenMenu
│   │   ├── sections/   # Hero, WorkGrid, AboutBlock, ContactForm
│   │   └── ui/         # Button, Link, CustomCursor, Loader, ScrollIndicator
│   ├── hooks/          # 自定义 Hooks
│   │   ├── useScrollReveal.ts
│   │   ├── useParallax.ts
│   │   ├── useLenis.ts
│   │   └── useCustomCursor.ts
│   ├── lib/            # 工具函数 / 常量
│   │   ├── cn.ts       # classnames 工具
│   │   ├── constants.ts
│   │   └── types.ts
│   ├── styles/         # 全局样式 / 主题变量
│   │   ├── globals.css
│   │   └── fonts.css
│   └── content/        # 内容数据
│       ├── projects.json
│       └── siteConfig.json
├── AGENTS.md           # 本文件
├── design.md           # 设计文档
├── SKILL.md            # 技能定义
└── README.md

---

## 开发工作流

### 终端命令

bash
# 开发环境启动
npm run dev

# 生产构建
npm run build

# 代码检查
npm run lint

# 格式化
npm run format

# 类型检查
npm run type-check


### AI 代理工作流

当 AI 代理参与开发时，应遵循以下流程：

#### 阶段一：上下文加载

1. **阅读 design.md** — 首次参与必须先阅读设计文档，确保对视觉风格有统一理解
2. **阅读 AGENTS.md** — 了解编码规范和项目约定
3. **阅读 SKILL.md** — 了解可用技能和技术栈
4. **浏览现有代码** — 了解当前项目状态和已有组件

#### 阶段二：任务执行

5. **聚焦当前任务** — 一次只做一件事，完成任务后再推进下一步
6. **渐进式修改** — 大的变更先与用户沟通方案，再实施
7. **尊重现有代码** — 不要重构已有工作代码（除非明确要求）
8. **测试验证** — 对新增交互逻辑编写测试，或手动验证一致性

#### 阶段三：质量保障

9. **图片资源** — 不要生成虚假的图片内容；使用占位符（placeholder）直到真实资产就绪
10. **动效实现** — 优先使用 CSS 过渡 / 动画，其次才考虑 JS 动效库
11. **联系信息** — 使用占位符代替真实的电子邮件/电话号码，避免泄露
12. **提交前检查** — 检查 TypeScript 类型、Lighthouse 评分、移动端适配

### 沟通规范

- AI 代理在决策模糊时应主动向用户提出 A/B 方案，而非自行猜测
- 当发现代码中与 design.md 不符的地方时，应标记并询问用户
- 完成一个组件或页面后，用简洁总结告知用户新增/修改的内容
- 遇到阻塞问题时，清晰描述问题上下文和已尝试的解决方案

---

## 组件开发规范

### 组件文件结构

```tsx
// 1. 类型定义（Props 接口）
interface HeroSectionProps {
  title: string;
  subtitle?: string;
  backgroundVideo?: string;
  className?: string;
}

// 2. 组件函数
export default function HeroSection({
  title,
  subtitle,
  backgroundVideo,
  className,
}: HeroSectionProps) {
  return (
    <section className={cn('relative h-screen', className)}>
      {/* 背景 */}
      {backgroundVideo && (
        <video autoPlay muted loop playsInline className="absolute inset-0 object-cover">
          <source src={backgroundVideo} type="video/mp4" />
        </video>
      )}
      {/* 内容 */}
      <div className="relative z-10 flex h-full items-center justify-center">
        <h1 className="text-8xl font-bold tracking-tight">{title}</h1>
        {subtitle && <p className="mt-4 text-lg">{subtitle}</p>}
      </div>
    </section>
  );
}
```

### 客户端组件标记

- 任何使用 useState、useEffect、浏览器 API 或事件监听的组件，必须在文件顶部添加 "use client"
- 纯展示（无交互）组件使用服务端组件

---

## 性能预算

| 指标 | 目标值 |
|------|--------|
| 首屏内容渲染（FCP） | < 1.5s |
| 最大内容绘制（LCP） | < 2.5s |
| 首次输入延迟（FID） | < 100ms |
| 累积布局偏移（CLS） | < 0.1 |
| 总阻塞时间（TBT） | < 200ms |
| 页面总大小 | < 500KB（不含图片） |
| 字体文件 | < 100KB 每字重（WOFF2） |

---

## 已知约束

- 字体文件大小不超过 100KB（WOFF2 格式）以确保加载性能
- 首屏最大内容绘制（LCP）不超过 2.5 秒
- 所有页面可访问性需达到 WCAG 2.1 AA 标准
- 不使用外部图片 CDN（除非客户提供）
- 禁用 Google Fonts 等外部字体服务；使用自托管字体
- 不使用任何 jQuery 或依赖 jQuery 的第三方库
- 所有用户交互反馈必须在 100ms 内可见

---

## 参考链接

- 目标网站: https://studionamma.com/
- 设计文档: ./design.md
- 技能定义: ./SKILL.md

---

> 本文档针对 AI 代理（如 Codex、Cursor、Copilot）编写，用于确保协作开发者快速理解项目规范并高效贡献代码。
