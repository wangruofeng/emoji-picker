# emoji-picker — 项目约定（给 AI 协作时参考）

纯前端、单文件的 Emoji 搜索与复制工具。面向人类的说明见 `README.md`；本文件记录**改代码时必须知道的红线与约定**。项目与同级目录 `../json-viewer`、`../xml-viewer` 保持同一套设计与代码风格。

## 红线（不要破坏）

- **单文件、零构建、零依赖**：全部 HTML / CSS / JS 都在 `index.html` 一个文件里。**禁止**引入打包器（Vite/Webpack 等）、框架（React/Vue 等）、npm 依赖或构建步骤。新增能力用原生 JS 实现。
- **纯前端、无后端**：所有数据与计算在浏览器本地完成，不上传任何数据。
- 主题用根元素 `html.dark` 类切换，配色全部走 `:root` / `html.dark` 里的 CSS 变量。新增颜色请复用已有变量，不要硬编码。
- **渲染用户输入一律 `createElement` / `textContent`**，禁止用 `innerHTML` 拼接用户可控或动态内容（XSS 红线）。页头主题按钮的静态 SVG 图标常量除外。

## 文件结构

- `index.html` — 全部代码（结构 + 样式 + 脚本），内置 `EMOJI_DATA` / `EMOJI_NAMES` / `I18N` 数据。
- `favicon.svg` — 蓝紫渐变圆角方块 + 白色 `😀`。
- `manifest.webmanifest` + `sw.js` — PWA 清单与 Service Worker（离线缓存应用壳）。
- `README.md` / `README.en.md` — 面向用户的功能说明与在线访问地址（中 / 英）。
- `CLAUDE.md` — 本文件，记录红线、约定与数据结构。

## UI 约定

- **按钮文案保持极简**：图标已承担表意，文字尽量短（如「复制」）。
- 页头右侧三个图标按钮：GitHub 源码链接（仓库 `https://github.com/wangruofeng/emoji-picker`，新标签页打开）、语言切换（🌐，下拉选 7 种语言）、深浅色主题切换。
- 搜索框、分类 tab、Emoji 网格、详情面板按 json-viewer 风格使用卡片、阴影、圆角。

## 数据结构与新增 Emoji 约定

内置数据集 `EMOJI_DATA` 为对象数组，每个对象必须包含以下字段：

```js
{
  ch: '😀',                    // Emoji 字符
  name: 'grinning face',       // 英文 CLDR 短名，用于英文搜索
  cn: '嘿嘿',                   // 中文名，显示在 tooltip 与详情面板
  kw: ['笑', '笑脸', '开心'],    // 中文关键词数组，用于中文搜索
  cat: '笑脸情感'               // 分类，必须是下面 9 个之一
}
```

分类固定为：

- `笑脸情感`
- `人物手势`
- `动物自然`
- `食物饮料`
- `活动运动`
- `旅行地点`
- `物品工具`
- `符号标志`
- `旗帜`

### 新增 Emoji 时必须补全中文关键词

新增或修改条目时，必须同时补充 `kw` 中文关键词，确保：

1. 包含常见中文叫法与同义词（如 👍 的 kw 应包含“赞”“好”“顶”“厉害”）。
2. 包含字面组成部分（如 🍎 包含“苹果”“水果”“红色”）。
3. 英文名已覆盖在 `name` 中，无需在 `kw` 重复英文，但允许保留常见英文昵称。
4. 不要放无意义单字填充；关键词应能真实提升搜索命中率。

肤色可变 Emoji 的基字需要同时加入 `SKIN_EMOJI` Set（详情面板据此显示肤色切换）。

## 多语言与本地存储

- **界面文案** `I18N`：键 -> {语言代码: 文案}，含 `{x}`/`{n}` 占位符，由 `t(key, vars)` 取当前语言并替换。新增 UI 文案必须为全部 7 种语言补齐。
- **Emoji 本地化名** `EMOJI_NAMES`：{语言: {字符: 名称}}，覆盖 `zh-TW/ja/ko/th/ms`，取自 Unicode CLDR。`localName(item)` 回退顺序：当前语言映射 -> `cn`（zh-CN/zh-TW）-> `name`（en）。新增语言须建对应子字典。
- 支持语言见 `LANGS`（`zh-CN/zh-TW/en/ja/ko/th/ms`），选择存 `localStorage`：
  - `emoji-theme` 主题、`emoji-lang` 语言、`emoji-recent` 最近使用（上限 24，去重前置）、`emoji-favorites` 收藏列表。
- **收藏夹**：Emoji 格悬停显示星标，点击切换收藏；收藏独立于最近使用，在「收藏」tab 查看。`state.favs` 为字符数组，持久化到 `emoji-favorites`。星标点击带轻微弹 / 缩动效（`animateFavStar()`，约 180ms），系统开启「减少动态效果」时自动禁用。

## 在线地址

已部署到 Cloudflare Pages：https://emoji-picker.wangruofeng007.com/
