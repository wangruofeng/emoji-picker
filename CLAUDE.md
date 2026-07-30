# emoji-picker — 项目约定（给 AI 协作时参考）

纯前端、单文件的 Emoji 搜索与复制工具。面向人类的说明见 `README.md`；本文件记录**改代码时必须知道的红线与约定**。项目与同级目录 `../json-viewer`、`../xml-viewer` 保持同一套设计与代码风格。

## 红线（不要破坏）

- **单文件、零构建、零依赖**：全部 HTML / CSS / JS 都在 `index.html` 一个文件里。**禁止**引入打包器（Vite/Webpack 等）、框架（React/Vue 等）、npm 依赖或构建步骤。新增能力用原生 JS 实现。
- **纯前端、无后端**：所有数据与计算在浏览器本地完成，不上传任何数据。
- 主题用根元素 `html.dark` 类切换，配色全部走 `:root` / `html.dark` 里的 CSS 变量。新增颜色请复用已有变量，不要硬编码。
- **渲染用户输入一律 `createElement` / `textContent`**，禁止用 `innerHTML` 拼接用户可控或动态内容（XSS 红线）。页头主题按钮的静态 SVG 图标常量除外。

## 文件结构

- `index.html` — 全部代码（结构 + 样式 + 脚本），内置 `EMOJI_DATA` 数据集。
- `favicon.svg` — 蓝紫渐变圆角方块 + 白色 `😀`。
- `.github/workflows/deploy.yml` — GitHub Pages 部署：仓库根即站点根，push 到 `main` 自动部署。
- `README.md` — 面向用户的功能说明与在线访问地址。
- `CLAUDE.md` — 本文件，记录红线、约定与数据结构。

## UI 约定

- **按钮文案保持极简**：图标已承担表意，文字尽量短（如「复制」）。
- 页头右侧两个图标按钮：GitHub 源码链接（仓库 `https://github.com/wangruofeng/emoji-picker`，新标签页打开）、深浅色主题切换。
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

## 在线地址

已部署到 GitHub Pages：https://blog.wangruofeng007.com/emoji-picker/
