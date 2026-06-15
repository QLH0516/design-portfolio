# Studio Namma 风格网站开发技能定义 (SKILL.md)

---

## 技能名称

studio-namma-web — 仿 Studio Namma 风格的创意工作室网站开发

---

## 适用场景

本技能适用于以下任务：

- 构建类似 studionamma.com 的创意工作室品牌官网
- 开发和实现极简主义设计风格的网站页面
- 实现具有叙事驱动体验的滚动互动网站
- 添加平滑页面过渡和视差滚动效果
- 构建具有自定义光标和微交互动效的品牌体验
- 实现全屏覆盖式菜单和高级导航交互
- 构建高对比度黑白 + 强调色的视觉系统

---

## 技术栈

| 领域 | 推荐技术 | 版本要求 |
|------|----------|----------|
| 框架 | Next.js 14+ (App Router) | >= 14.0 |
| 语言 | TypeScript | strict 模式 |
| 样式 | Tailwind CSS v3 + CSS Custom Properties | >= 3.3 |
| 动效 | GSAP + ScrollTrigger | >= 3.12 |
| 平滑滚动 | Lenis | >= 1.0 |
| 图像 | next/image | 内置于 Next.js |
| 字体 | 自托管 WOFF2 + @font-face | — |
| 工具类 | clsx + tailwind-merge | 最新版 |
| 部署 | Vercel | — |

---

## 快速开始

bash
# 创建 Next.js 项目
npx create-next-app@latest . --typescript --tailwind --app --src-dir --import-alias "@/*"

# 安装动效依赖
npm install gsap @studio-freight/lenis clsx tailwind-merge

# 安装类型提示（可选）
npm install -D @types/gsap


---

## 实现清单

### □ 阶段一：项目初始化与全局样式

- [ ] 运行 create-next-app 初始化项目
- [ ] 配置 tailwind.config.ts（颜色扩展、字体族、断点）
- [ ] 创建全局 CSS 自定义属性（globals.css）
- [ ] 设置自托管字体（fonts.css + @font-face）
- [ ] 配置 tsconfig.json path aliases
- [ ] 安装并配置 Lenis 平滑滚动
- [ ] 创建 cn() 工具函数（clsx + tailwind-merge 封装）

### □ 阶段二：布局组件

- [ ] **Header** — 固定定位，透明背景，滚动后变半透明/白色
- [ ] **FullscreenMenu** — 全屏覆盖式菜单，展开收起动画
- [ ] **Footer** — 极简页脚，社交链接 + Email + 版权信息
- [ ] **根布局（RootLayout）** — 全局字体、元数据、SEO 配置

### □ 阶段三：页面区块组件

- [ ] **HeroSection** — 全屏视口高度，大标题 + 背景视频/图片 + 滚动指示器
- [ ] **WorkGrid** — 2列网格项目展示，hover 交互
- [ ] **ProjectCard** — 图片 + 标题 + 类别标签，hover 动画
- [ ] **ProjectDetailLayout** — 沉浸式叙事布局
- [ ] **AboutSection** — 工作室介绍 + 团队 + 客户名录
- [ ] **ContactForm** — 极简联系表单，无多余装饰
- [ ] **ScrollIndicator** — 底部箭头动画引导用户滚动

### □ 阶段四：交互与动效

- [ ] **自定义光标** — 圆形光环跟随鼠标，触摸设备自动隐藏
- [ ] **滚动揭示动画** — useScrollReveal hook（Intersection Observer）
- [ ] **视差效果** — useParallax hook（不同速度的多层滚动）
- [ ] **GSAP 滚动触发** — 复杂时间线动画接入 ScrollTrigger
- [ ] **全屏菜单动画** — 菜单项展开时的交错动画
- [ ] **图片揭示动画** — 滚动时 clip-path 遮罩揭示
- [ ] **页面过渡** — 页面切换间的平滑过渡（Framer Motion 或 CSS 动画）
- [ ] **Hover 微交互** — 链接下划线、图片缩放、色彩切换

### □ 阶段五：页面组装

- [ ] **首页（/）** — Hero + 精选项目 + 工作室简介
- [ ] **项目列表页（/work）** — 所有项目的网格展示
- [ ] **项目详情页（/work/[slug]）** — 动态路由，单个项目详情
- [ ] **关于页（/about）** — 工作室信息 + 团队展示
- [ ] **联系页（/contact）** — 联系表单 + 社交链接
- [ ] **404 页面** — 简洁 404 错误页

### □ 阶段六：性能与优化

- [ ] 字体子集化与预加载（preload + font-display: swap）
- [ ] 图片优化（next/image + webp + blurDataURL）
- [ ] 代码分割（dynamic imports + React.lazy）
- [ ] 元数据与 SEO（generateMetadata + JSON-LD）
- [ ] 可访问性检查（键盘导航、ARIA 标签、焦点管理）
- [ ] Lighthouse 评分 > 90
- [ ] 移动端响应式验证

---

## 主题变量（CSS）

css
:root {
  /* === 颜色 === */
  --color-bg: #fafafa;
  --color-bg-dark: #0a0a0a;
  --color-text: #0a0a0a;
  --color-text-dark: #fafafa;
  --color-accent: #c92a2a;
  --color-accent-hover: #e03e3e;
  --color-gray-100: #f5f5f5;
  --color-gray-300: #cccccc;
  --color-gray-400: #999999;
  --color-gray-700: #333333;

  /* === 排版 === */
  --font-sans: "NeueHaasGrotesk", "Inter Display", "Helvetica Neue", sans-serif;
  --font-size-h1: clamp(3.5rem, 10vw, 7rem);
  --font-size-h2: clamp(2rem, 5vw, 4rem);
  --font-size-body: clamp(1rem, 1.5vw, 1.25rem);
  --font-size-small: 0.75rem;
  --font-weight-light: 300;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --leading-tight: 1.05;
  --leading-relaxed: 1.7;
  --tracking-tight: -0.02em;
  --tracking-wide: 0.15em;

  /* === 间距 === */
  --section-gap: clamp(4rem, 12vh, 10rem);
  --page-padding: clamp(1rem, 5vw, 3rem);
  --grid-gap: clamp(2rem, 4vw, 4rem);

  /* === 动画缓动 === */
  --ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1);
  --ease-in-out: cubic-bezier(0.76, 0, 0.24, 1);
  --ease-out-quart: cubic-bezier(0.25, 1, 0.5, 1);
  --duration-slow: 1.2s;
  --duration-medium: 0.8s;
  --duration-fast: 0.4s;

  /* === 布局 === */
  --content-max-width: 1200px;
  --header-height: 80px;
}


---

## 自定义 Hooks 模板

### useScrollReveal（Intersection Observer 方案）

typescript
"use client";

import { useEffect, useRef, useState } from "react";

interface ScrollRevealOptions {
  threshold?: number;
  rootMargin?: string;
  once?: boolean;
}

export function useScrollReveal<T extends HTMLElement = HTMLDivElement>(
  options: ScrollRevealOptions = {}
) {
  const { threshold = 0.1, rootMargin = "0px 0px -100px 0px", once = true } = options;
  const ref = useRef<T>(null);
  const [isVisible, setIsVisible] = useState(false);

  useEffect(() => {
    const el = ref.current;
    if (!el) return;

    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          setIsVisible(true);
          if (once) observer.unobserve(el);
        } else if (!once) {
          setIsVisible(false);
        }
      },
      { threshold, rootMargin }
    );

    observer.observe(el);
    return () => observer.disconnect();
  }, [threshold, rootMargin, once]);

  return { ref, isVisible };
}


### useLenis（平滑滚动）

typescript
"use client";

import { useEffect, useRef } from "react";
import Lenis from "@studio-freight/lenis";

export function useLenis() {
  const lenisRef = useRef<Lenis | null>(null);

  useEffect(() => {
    const lenis = new Lenis({
      duration: 1.2,
      easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
      orientation: "vertical",
      smoothWheel: true,
    });

    function raf(time: number) {
      lenis.raf(time);
      requestAnimationFrame(raf);
    }

    requestAnimationFrame(raf);
    lenisRef.current = lenis;

    return () => lenis.destroy();
  }, []);

  return lenisRef;
}


### useCustomCursor

typescript
"use client";

import { useEffect, useRef } from "react";

export function useCustomCursor() {
  const cursorRef = useRef<HTMLDivElement>(null);
  const isTouchDevice =
    typeof window !== "undefined" && "ontouchstart" in window;

  useEffect(() => {
    if (isTouchDevice) return;

    const handleMove = (e: MouseEvent) => {
      if (cursorRef.current) {
        cursorRef.current.style.transform = `translate(${e.clientX}px, ${e.clientY}px)`;
      }
    };

    const handleLeave = () => {
      if (cursorRef.current) cursorRef.current.style.opacity = "0";
    };

    const handleEnter = () => {
      if (cursorRef.current) cursorRef.current.style.opacity = "1";
    };

    window.addEventListener("mousemove", handleMove);
    document.addEventListener("mouseleave", handleLeave);
    document.addEventListener("mouseenter", handleEnter);

    return () => {
      window.removeEventListener("mousemove", handleMove);
      document.removeEventListener("mouseleave", handleLeave);
      document.removeEventListener("mouseenter", handleEnter);
    };
  }, [isTouchDevice]);

  return { cursorRef, isTouchDevice };
}


---

## 组件模板

### 客户端组件（含交互）

tsx
"use client";

interface ProjectCardProps {
  title: string;
  category: string;
  imageSrc: string;
  slug: string;
}

export default function ProjectCard({
  title,
  category,
  imageSrc,
  slug,
}: ProjectCardProps) {
  return (
    <article className="group cursor-pointer">
      <div className="overflow-hidden">
        <img
          src={imageSrc}
          alt={title}
          className="h-[60vh] w-full object-cover transition-transform duration-700 group-hover:scale-105"
          loading="lazy"
        />
      </div>
      <div className="mt-4 flex items-baseline justify-between">
        <h3 className="text-2xl font-bold transition-colors duration-300 group-hover:text-[var(--color-accent)]">
          {title}
        </h3>
        <span className="text-xs uppercase tracking-[0.15em] text-[var(--color-gray-400)]">
          {category}
        </span>
      </div>
    </article>
  );
}


### 服务端组件（纯展示）

tsx
interface AboutBlockProps {
  description: string;
  stats: { label: string; value: string }[];
}

export default function AboutBlock({ description, stats }: AboutBlockProps) {
  return (
    <section className="mx-auto grid max-w-[var(--content-max-width)] grid-cols-1 gap-16 md:grid-cols-12">
      <div className="md:col-span-7">
        <p className="text-lg leading-relaxed">{description}</p>
      </div>
      <div className="md:col-span-4 md:col-start-9">
        {stats.map((stat) => (
          <div key={stat.label} className="border-t border-[var(--color-gray-300)] py-4">
            <span className="block text-4xl font-bold">{stat.value}</span>
            <span className="mt-1 block text-xs uppercase tracking-[0.15em]">
              {stat.label}
            </span>
          </div>
        ))}
      </div>
    </section>
  );
}


---

## 设计参考

请参阅同目录下的 design.md 文件获取完整的视觉设计语言分析，包括：

- 色彩系统与配色策略（含具体色值和对比度要求）
- 排版层级与字体选择（含备选字体方案）
- 网格系统与布局模式（含偏移布局和全出血策略）
- 图像/视频风格指南（含占位策略）
- 交互与动效设计原则（含性能约束）
- 具体页面逐区块参照（Hero、项目网格、关于区、联系区）
- 可交付组件清单（含优先级排序）

AGENTS.md 文件中包含了编码规范、项目结构和 AI 代理协作流程。

---

## 验证标准

实现完成后，逐项检查以下标准：

### 视觉一致性
- [ ] 页面色彩与 design.md 规范一致
- [ ] 排版层级与规范一致（clamp 值、行高、字重）
- [ ] 间距和留白与规范一致
- [ ] 强调色使用克制，仅用于关键交互元素

### 交互完整性
- [ ] 平滑滚动流畅运行（Lenis）
- [ ] 滚动揭示动画按预期触发
- [ ] 自定义光标在桌面端显示，触摸设备隐藏
- [ ] 全屏菜单展开/收起动画平滑
- [ ] Hover 微交互状态正确变化
- [ ] 页面切换无闪烁

### 性能
- [ ] Lighthouse 性能评分 > 90
- [ ] 所有图片使用了 next/image
- [ ] 字体文件预加载，无 FOUT/FOIT
- [ ] 动画维持 60fps（Chrome DevTools Performance 面板验证）

### 可访问性
- [ ] 键盘导航完整（Tab、Enter、Escape）
- [ ] 全屏菜单支持 Escape 关闭
- [ ] 所有图片包含有意义的 alt 属性
- [ ] ARIA 标签应用于自定义交互组件
- [ ] 颜色对比度满足 WCAG AA（文本 4.5:1，大文本 3:1）

### 响应式
- [ ] 桌面端（1440px+）布局完整
- [ ] 平板端（768px）无布局断裂
- [ ] 移动端（375px）触摸友好，间距合理
- [ ] 全屏菜单在移动端正常显示

---

## 常见问题与解决方案

| 问题 | 解决方案 |
|------|----------|
| Lenis 与 ScrollTrigger 冲突 | 使用 Lenis 的 lenis-scroll 事件触发 ScrollTrigger.update() |
| 自定义光标在 iframe 内失效 | 无解，使用 CSS cursor: none 并添加 fallback |
| 字体加载闪烁（FOUT） | 使用 font-display: swap + 预加载 + 字体回退期间隐藏文本 |
| 全屏菜单滚动穿透 | 菜单打开时 body 设置 overflow: hidden |
| next/image 外部域名报错 | 在 next.config.js 的 images.remotePatterns 中添加域名 |
| Tailwind CSS 自定义颜色未生效 | 检查 tailwind.config.ts 中 extend.colors 配置 |

---

> 本技能文件定义了对 Studio Namma 风格网站的完整实现路径。配合 design.md 和 AGENTS.md 使用，可实现高质量的品牌网站开发。
