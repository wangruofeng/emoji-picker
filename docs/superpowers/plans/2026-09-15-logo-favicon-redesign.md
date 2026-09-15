# Logo 与 Favicon 重设计 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 将已确认的「跳跳心 + 三条柔弧」原创标识接入页面 Header、favicon 和 PWA。

**Architecture:** 以独立 `logo.svg` 保存品牌母版，以小尺寸优化的 `favicon.svg` 服务浏览器与 PWA；Header 内嵌同构 SVG，以保证单文件页面离线打开时仍完整显示。只改品牌图形及其样式，不触碰产品功能逻辑。

**Tech Stack:** 原生 HTML、CSS、SVG、Web App Manifest

**Spec:** `docs/superpowers/specs/2026-09-15-logo-favicon-redesign.md`

## Global Constraints

- 使用暖橙圆脸、两颗跳动粉红爱心与三条圆头柔弧。
- Logo 不使用系统 Emoji 字形，不使用渐变或阴影。
- 保持现有页面功能、文字和蓝紫 UI 主题不变。

---

### Task 1: 创建品牌 SVG 资产

**Files:**
- Create: `logo.svg`
- Modify: `favicon.svg`

**Interfaces:**
- Consumes: 72 × 72 的「跳跳心」视觉规范
- Produces: 页面可复用 Logo 母版与浏览器/PWA 图标

- [x] **Step 1:** 用 SVG 创建暖橙圆脸、两颗粉红爱心和三条圆头柔弧。
- [x] **Step 2:** 为 favicon 加粗面部线条并保持 `viewBox="0 0 72 72"`。
- [x] **Step 3:** 运行 `xmllint --noout logo.svg favicon.svg`，预期两个文件均无输出且退出码为 0。

### Task 2: 接入页面 Header

**Files:**
- Modify: `index.html`

**Interfaces:**
- Consumes: 与 `logo.svg` 同构的 SVG 路径
- Produces: 首屏稳定呈现的 Header 品牌标识

- [x] **Step 1:** 将 `.logo .mark` 从带背景的文字容器改为 30 × 30 的 SVG 容器。
- [x] **Step 2:** 用带 `aria-label="Emoji 选择器 Logo"` 的内嵌 SVG 替换系统 😀 字形。
- [x] **Step 3:** 搜索 `😀` 与旧渐变色，确认 Header 标识不再依赖二者。

### Task 3: 一致性与回归验证

**Files:**
- Verify: `index.html`
- Verify: `manifest.webmanifest`
- Verify: `logo.svg`
- Verify: `favicon.svg`

**Interfaces:**
- Consumes: 已接入的页面与 SVG 资产
- Produces: 可审阅的验证结果

- [x] **Step 1:** 检查 manifest 的 icon 路径存在且仍为 SVG。
- [x] **Step 2:** 启动本地静态服务器并在浏览器检查 Header、favicon、深浅色模式和移动端 Header。
- [x] **Step 3:** 查看 `git diff --check` 与聚焦 diff，确认没有空白错误或无关改动。
