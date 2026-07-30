# Emoji 展示选择器

**[English](./README.en.md)** | 简体中文

一个纯前端的单文件 Emoji 搜索与复制工具，双击 `index.html` 即可使用，无需安装、无需后端、无任何外部依赖。

## 功能特性

- 🌐 **多语言界面**：支持简体中文、繁体中文、英语、日语、韩语、泰语、马来语 7 种语言切换，语言偏好自动保存。Emoji 名称取自 Unicode CLDR 官方本地化标注。
- 🔍 **多语言 / 关键词搜索**：输入“笑”“heart”“火”等即时过滤 800+ Emoji，搜索随当前语言适配。
- 🗂️ **分类浏览**：笑脸情感、人物手势、动物自然、食物饮料、活动运动、旅行地点、物品工具、符号标志、旗帜九大分类，以及“最近使用”。
- 📋 **一键复制**：点击 Emoji 格子即可复制字符，并自动记录到最近使用（`localStorage emoji-recent`，上限 24 个，去重前置）。
- 📊 **码点详情**：点击后在详情面板展示 Unicode 码点、UTF-8 字节、HTML 实体、CSS content、JS 转义，每项均可单独复制。
- 🏻 **肤色变体**：对支持肤色的手势类 Emoji，详情面板提供 6 种肤色快速切换复制。
- 🌓 **深浅色主题**：一键切换，偏好保存在 `localStorage emoji-theme`。
- 📱 **响应式布局**：桌面端详情面板在右侧，移动端在底部。

## 使用方式

直接用浏览器打开 `index.html` 即可：

```bash
open index.html        # macOS
# 或拖入浏览器
```

在搜索框输入中文关键词或英文名即可快速定位；点击任意 Emoji 复制并查看详情。

## 技术说明

- 单一 HTML 文件，原生 HTML / CSS / JavaScript，零依赖、零构建步骤。
- Emoji 数据内嵌为 JS 常量，所有解析与渲染均在浏览器本地完成，不上传任何数据。
- 动态渲染一律使用 `createElement` / `textContent`，避免 XSS 注入风险。

## 在线访问

已通过 GitHub Pages 部署，可直接访问：

🔗 **https://blog.wangruofeng007.com/emoji-picker/**

源码仓库：https://github.com/wangruofeng/emoji-picker
