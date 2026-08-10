# Emoji Picker

English | **[简体中文](./README.md)**

A pure front-end, single-file Emoji search and copy tool. Just double-click `index.html` to use it — no installation, no back-end, and zero external dependencies.

When served over HTTPS or localhost, it also supports installation as a PWA and caches its app shell for offline use.

## Features

- 🌐 **Multi-language UI**: Switch among 7 languages — Simplified Chinese, Traditional Chinese, English, Japanese, Korean, Thai, and Malay. Your language choice is saved automatically. Emoji names come from the official Unicode CLDR localized annotations.
- 🔍 **Multi-language & keyword search**: Instantly filter 800+ emoji by typing terms such as “smile”, “heart”, or “fire”; search adapts to the active language.
- 🗂️ **Browse by category**: Nine categories — Smileys & Emotion, People & Body, Animals & Nature, Food & Drink, Activities, Travel & Places, Objects, Symbols, Flags — plus a “Recent” view.
- 📋 **One-click copy**: Click any emoji cell to copy the character, which is also recorded to the recent list (`localStorage emoji-recent`, capped at 24, de-duplicated and moved to front).
- ⭐ **Favorites**: Hover an emoji and click the star in the corner to favorite it; favorites are saved in `localStorage emoji-favorites` and shown in a dedicated “Favorites” view.
- 📊 **Codepoint details**: After clicking, the detail panel shows the Unicode codepoint, UTF-8 bytes, HTML entity, CSS `content`, and JS escape — each individually copyable.
- 🏻 **Skin-tone variants**: For gesture emoji that support skin tones, the detail panel offers 6 tones for quick switching and copying.
- 🌓 **Light / dark theme**: One-click toggle; the preference is saved in `localStorage emoji-theme`.
- 📱 **Responsive layout**: The detail panel sits on the right on desktop and slides to the bottom on mobile.

## Usage

Open `index.html` directly in your browser:

```bash
open index.html        # macOS
# or drag it into your browser
```

Type a name or keyword in the search box to quickly locate an emoji; click any emoji to copy it and view its details. Use the 🌐 button in the header to switch the interface language.

## Technical Notes

- A single HTML file built with native HTML / CSS / JavaScript — zero dependencies and zero build steps.
- Emoji data is embedded as a JavaScript constant; all parsing and rendering happen locally in the browser. No data is ever uploaded.
- The current Emoji data primarily comes from the [official Unicode Emoji 17.0 data directory](https://www.unicode.org/Public/17.0.0/emoji/).
- Dynamic rendering always uses `createElement` / `textContent` to avoid XSS injection risks.

## Live Demo

Deployed via Cloudflare Pages and available here:

🔗 **https://emoji-picker.wangruofeng007.com/**

Source repository: https://github.com/wangruofeng/emoji-picker
