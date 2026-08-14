---
version: alpha
name: Emoji Picker
description: 纯前端单文件 Emoji 搜索与复制工具的视觉规范；GitHub 风格浅/深双主题，靛蓝强调色。
colors:
  # 语义色板（浅色主题）
  bg: "#f6f7f9"
  panel: "#ffffff"
  border: "#e5e7eb"
  border-strong: "#d1d5db"
  text: "#1f2328"
  text-muted: "#6b7280"
  text-faint: "#9ca3af"
  primary: "#4f46e5"
  primary-hover: "#4338ca"
  primary-soft: "#eef2ff"
  danger: "#dc2626"
  danger-soft: "#fef2f2"
  success: "#16a34a"
  star: "#f59e0b"
  # 品牌渐变（logo / favicon / og 图）
  brand-from: "#2563eb"
  brand-to: "#7c3aed"
  # 强调色之上的文字
  on-primary: "#ffffff"
  # 深色主题对应值
  dark-bg: "#0d1117"
  dark-panel: "#161b22"
  dark-border: "#30363d"
  dark-border-strong: "#484f58"
  dark-text: "#e6edf3"
  dark-text-muted: "#9198a1"
  dark-text-faint: "#6e7681"
  dark-primary: "#818cf8"
  dark-primary-hover: "#a5b4fc"
  dark-primary-soft: "#1e1b4b"
  dark-danger: "#f87171"
  dark-danger-soft: "#2a1a1c"
  dark-success: "#3fb950"
  dark-star: "#fbbf24"
typography:
  body-md:
    fontFamily: -apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", Roboto, Helvetica, Arial, sans-serif
    fontSize: 14px
    fontWeight: 400
    lineHeight: 1.6
  body-sm:
    fontFamily: -apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", Roboto, Helvetica, Arial, sans-serif
    fontSize: 13px
    fontWeight: 400
    lineHeight: 1.6
  label-sm:
    fontFamily: -apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", Roboto, Helvetica, Arial, sans-serif
    fontSize: 12px
    fontWeight: 400
    lineHeight: 1.4
  title-md:
    fontFamily: -apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", Roboto, Helvetica, Arial, sans-serif
    fontSize: 15px
    fontWeight: 600
    lineHeight: 1.4
  section-caps:
    fontFamily: -apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", Roboto, Helvetica, Arial, sans-serif
    fontSize: 13px
    fontWeight: 600
    letterSpacing: 0.03em
  code-md:
    fontFamily: ui-monospace, SFMono-Regular, "SF Mono", Menlo, Consolas, "Liberation Mono", monospace
    fontSize: 13px
    fontWeight: 400
    lineHeight: 1.4
rounded:
  sm: 4px
  md: 6px
  lg: 8px
  xl: 10px
  full: 9999px
spacing:
  xs: 3px
  sm: 8px
  md: 10px
  lg: 12px
  xl: 20px
  xxl: 28px
  page-x: 20px
  grid-gap: 8px
  grid-cell: 56px
components:
  emoji-cell:
    backgroundColor: "{colors.panel}"
    borderColor: "{colors.border}"
    textColor: "{colors.text}"
    rounded: "{rounded.xl}"
    size: "{spacing.grid-cell}"
  emoji-cell-hover:
    borderColor: "{colors.primary}"
    transform: translateY(-2px)
  tab-btn-active:
    backgroundColor: "{colors.primary-soft}"
    textColor: "{colors.primary}"
    borderColor: "{colors.primary}"
    rounded: "{rounded.lg}"
  input-focus:
    borderColor: "{colors.primary}"
    boxShadow: "0 0 0 3px {colors.primary-soft}"
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-primary}"
    borderColor: "{colors.primary}"
    rounded: "{rounded.lg}"
  tooltip:
    backgroundColor: "{colors.text}"
    textColor: "{colors.panel}"
    rounded: "{rounded.md}"
  toast:
    backgroundColor: "{colors.text}"
    textColor: "{colors.panel}"
    rounded: "{rounded.lg}"
---

# Emoji Picker 设计规范

本文件遵循 [DESIGN.md 格式规范](https://github.com/google-labs-code/design.md)，描述本项目的视觉识别系统。CSS 变量（`index.html` 内 `:root` / `html.dark`）是 token 的最终实现，本文件是其人类可读的映射与 rationale。

## Overview

**Emoji Picker** 是一个纯前端、单文件的 Emoji 搜索与复制工具，与同目录的 json-viewer / xml-viewer 保持同一套设计语言：**GitHub 风格的克制工具美学**——卡片化布局、轻阴影、细边框、低饱和中性底色上以单一强调色驱动全部交互。

- **个性**：工程感、干净、高密度但不拥挤。Emoji 网格是绝对主角，UI 退居幕后。
- **受众**：开发者和重度 IM 用户，需要快速搜索、复制字符并查询码点。
- **双主题**：浅色（默认）与深色通过 `html.dark` 类整体切换，全部颜色走 CSS 变量，禁止硬编码。
- **交互色哲学**：全站只有一个强调色（当前为靛蓝 Indigo），hover 边框、tab 激活、输入框聚焦、主按钮、链接共用，保证视觉一致性。

## Colors

调色板为「GitHub 式中性底 + 单一靛蓝强调色」，浅/深两套一一对应。

### 浅色主题（默认，`:root`）

- **bg (#f6f7f9)**：冷灰页面底色，比纯白柔和，让白色卡片浮起。
- **panel (#ffffff)**：所有卡片、工具栏、弹层的表面色。
- **border (#e5e7eb) / border-strong (#d1d5db)**：细边框两档，后者用于 hover 与滚动条。
- **text (#1f2328) / text-muted (#6b7280) / text-faint (#9ca3af)**：正文 / 次要说明 / 占位与禁用三档灰阶。
- **primary (#4f46e5)**：靛蓝，全站唯一交互色——hover 边框、tab 激活、聚焦、链接、主按钮。hover 加深为 #4338ca，柔和底为 #eef2ff。
- **danger (#dc2626) / danger-soft (#fef2f2)**：删除类操作及其悬停底色。
- **success (#16a34a)**：复制成功等正向反馈。
- **star (#f59e0b)**：收藏星标专属琥珀色，不作他用。
- **brand-from (#2563eb) → brand-to (#7c3aed)**：蓝紫品牌渐变，仅用于 logo 标记、favicon、og 图，与交互色分离。
- **on-primary (#ffffff)**：强调色按钮上的文字。

### 深色主题（`html.dark`）

- 表面系：bg #0d1117 / panel #161b22 / border #30363d / border-strong #484f58（GitHub dark 系）。
- 文字系：#e6edf3 / #9198a1 / #6e7681。
- 交互色提亮：primary #818cf8（hover #a5b4fc，soft #1e1b4b）；danger #f87171；success #3fb950；star #fbbf24。

## Typography

单一系统 UI 字体栈（-apple-system 起头，中文字体 PingFang SC / Microsoft YaHei 兜底），代码与编码值用等宽栈。没有衬线、没有展示字体——工具不需要。

- **正文 14px**：全局默认；次要场景降至 13px / 12px。
- **分组标题 15px/600**：分类 sticky 标题。
- **小节标题 13px/600 大写 +0.03em**：详情面板「编码信息」等。
- **代码 13px 等宽**：Unicode / UTF-8 / HTML / CSS / JS 转义值。

## Layout

单列应用壳：header（logo + 主题/语言/源码按钮）→ toolbar（搜索 + 统计）→ tabs（分类）→ 滚动主区（分类分节的 emoji 网格 + 右侧详情面板双栏，≤768px 折叠为单栏）。

- 网格 `repeat(auto-fill, minmax(56px, 1fr))`、间距 8px；移动端 min 52px、间距 6px。
- 分组标题 sticky 置顶，背景为 `bg`，滚动时 pin 在内容区顶部。
- 页面水平 padding 20px（移动端 14px）。

## Elevation & Depth

深度靠**细边框 + 轻阴影**双信号，不靠重投影：

- **shadow**（`0 1px 3px rgba(0,0,0,.06)` 浅色）：卡片静止态，几乎不可见的落尘感。
- **shadow-hover**（`0 4px 12px` 强调色 15% 透明度）：emoji 卡片悬停，阴影染色跟随强调色。
- **shadow-lg**（`0 8px 24px rgba(0,0,0,.2)`）：toast 等浮动层。
- 深色主题下阴影透明度整体加重（.4 / .2）补偿对比度。

## Shapes

现代圆角体系，四档 + 全圆：

- **4px**：kbd 徽标等微小元素。
- **6px**：tooltip、代码值框、mini 按钮。
- **8px**：按钮、输入框、图标按钮、toast。
- **10px（`--radius`）**：emoji 卡片、详情面板、弹层卡。
- **9999px**：分类计数胶囊、info-tag。

## Components

- **Emoji 卡片**：方形（aspect-ratio 1），panel 底 + border 边框 + xl 圆角；hover 上浮 2px、边框转 primary、阴影染色。右上角收藏星标（琥珀色，hover 显现）。
- **分类 tab**：胶囊按钮，激活态 primary-soft 底 + primary 文字与边框。
- **搜索输入**：bg 底 + border 边框；聚焦 primary 边框 + 3px primary-soft 光环。
- **主按钮**（zoom primary / 分享）：primary 实底 + on-primary 文字。
- **Tooltip / Toast**：反色（text 底 + panel 字），md/lg 圆角，toast 底部居中浮现。

## Do's and Don'ts

- Do 全站只用一个强调色；新增交互态复用 `--accent` 系列变量
- Do 新增颜色先找 `:root` / `html.dark` 是否已有可复用变量，两套主题同时补
- Don't 在样式区硬编码十六进制色值（品牌渐变变量 `--brand-from/to` 除外，且仅用于品牌标识）
- Don't 让强调色与品牌渐变混用——渐变只属于 logo/favicon/og，交互永远用纯色 accent
- Don't 对用户可控内容使用 innerHTML 拼接（XSS 红线，见 CLAUDE.md）
- Don't 引入第二套阴影写法；用 `--shadow` / `--shadow-hover` / `--shadow-lg` 三档
