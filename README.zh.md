<p align="center">
  <img src="https://raw.githubusercontent.com/zkreations/tooltips/master/.github/tooltips.svg?sanitize=true" width="128" alt="tooltips" />
  <h1 align="center">Tooltips</h1>
  <p align="center">
    <a href="README.md">English</a> ·
    <a href="README.es.md">Español</a> ·
    <a href="README.fr.md">Français</a> ·
    <a href="README.pt.md">Português</a> ·
    <strong>中文</strong> ·
    <a href="README.ja.md">日本語</a>
    —
    <a href="https://zkreations.github.io/tooltips/">Demo</a>
  </p>
</p>

<p align="center">纯 CSS 工具提示库。无 JavaScript、无依赖、无需配置，支持现代浏览器并为不兼容的浏览器提供回退，压缩后约 0.5 KB（Brotli）</p>

<p align="center">
  <a href="https://www.jsdelivr.com/package/npm/@zkreations/tooltips"><img src="https://img.shields.io/jsdelivr/npm/hm/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=f97316" alt="jsdelivr"></a>
  <a href="https://www.npmjs.com/package/@zkreations/tooltips"><img src="https://img.shields.io/npm/v/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=a855f7" alt="npmjs"></a>
  <a href="https://www.npmjs.com/package/@zkreations/tooltips"><img src="https://img.shields.io/npm/l/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=6366f1" alt="license"></a>
</p>

## 为什么选择这个库而不是基于 JavaScript 的方案

大多数工具提示库需要 JavaScript 来计算位置、绑定事件监听器并管理显示状态。这个库不做任何这些——所有行为都在 CSS 中声明。

## 特性

* **纯 CSS。** 无 JavaScript、无依赖、无需配置。
* **原生定位。** 使用 CSS Anchor Positioning 计算位置，并在空间不足时自动切换方向。
* **代码最小化。** 样式表仅包含基础行为所需的规则，不包含你可能不会用到的位置、样式或动画类。
* **通过 CSS 配置。** 每个工具提示可以根据项目需求，通过 CSS 自定义属性定义其位置、外观和动画。
* **无布局偏移。** 定位发生在浏览器计算布局期间，不在渲染后测量 DOM。
* **无障碍访问。** 使用 `aria-label` 作为内容，并在 `:focus` 时显示工具提示。
* **自动回退。** 不支持 CSS Anchor Positioning 的浏览器使用顶部居中的绝对定位。

> [!IMPORTANT]
> CSS Anchor Positioning 是一项相对较新的浏览器功能。不支持它的浏览器将收到可预测的回退方案（顶部居中气泡，绝对定位），而非动态定位。

## 安装

### npm

```bash
npm i @zkreations/tooltips
```

### 框架和打包工具

该包将其压缩的 CSS 作为默认样式入口导出：

```js
import '@zkreations/tooltips';
```

在应用程序入口点导入一次：

**Next.js**
```tsx
// app/layout.tsx or pages/_app.tsx
import '@zkreations/tooltips';
```

**Astro**
```astro
---
import '@zkreations/tooltips';
---
```

同样的导入方式适用于 Vite、Nuxt、SvelteKit 以及其他支持从包导入 CSS 的打包工具。如果打包工具无法解析包的样式入口，请直接导入文件：

```js
import '@zkreations/tooltips/index.min.css';
```

不要同时导入两个路径——它们包含相同的样式表。

### Sass

仅在项目需要编译源代码时使用 Sass 入口：

```scss
@use '@zkreations/tooltips/scss/tooltip';
```

在这种情况下，不要同时导入包的 CSS。大多数项目应使用编译后的 CSS 入口。

### CDN

```html
<link href="https://cdn.jsdelivr.net/npm/@zkreations/tooltips@5/index.min.css" rel="stylesheet"/>
```

## 使用方法

将 `.tooltip` 类和 `aria-label` 属性添加到任意 HTML 元素：

```html
<button type="button" class="tooltip" aria-label="你好，世界！">
  悬停或聚焦我
</button>
```

### 定位

工具提示默认显示在顶部（`block-start`），当空间不足时自动切换（`flip-block, flip-inline`）：

```css
.tooltip::before {
  position-area: var(--tooltip-area, block-start);
  position-try-fallbacks: var(--tooltip-fallbacks, flip-block, flip-inline);
}
```

要设置自定义位置，覆盖 `--tooltip-area`：

```css
.tooltip--right  { --tooltip-area: inline-end; }
.tooltip--left   { --tooltip-area: inline-start; }
.tooltip--bottom { --tooltip-area: block-end; }
```

要固定位置且不自动切换：

```css
.tooltip--fixed-right {
  --tooltip-area: inline-end;
  --tooltip-fallbacks: none;
}
```

### 程序化显示

要在不悬停或聚焦的情况下显示工具提示，添加 `data-tooltip-visible`：

```html
<button type="button" class="tooltip" aria-label="活动通知" data-tooltip-visible>
  通知
</button>
```

## 自定义

覆盖 CSS 变量以调整外观：

| 变量 | 默认值 | 描述 |
| --- | --- | --- |
| `--tooltip-area` | `block-start` | 相对于锚点的位置区域 |
| `--tooltip-fallbacks` | `flip-block, flip-inline` | 被裁剪时的回退位置 |
| `--tooltip-gap` | `0.5rem` | 锚点与工具提示之间的间距 |
| `--tooltip-bg` | `rgb(0 0 0 / 90%)` | 背景颜色 |
| `--tooltip-color` | `#fff` | 文字颜色 |
| `--tooltip-font-size` | `0.875rem` | 字体大小 |
| `--tooltip-font-family` | `inherit` | 字体系列 |
| `--tooltip-line-height` | `1.5` | 行高 |
| `--tooltip-padding` | `0.5em 0.75em` | 气泡内边距 |
| `--tooltip-border` | `none` | 气泡边框 |
| `--tooltip-border-radius` | `0.25em` | 边框圆角 |
| `--tooltip-box-shadow` | `none` | 气泡阴影 |
| `--tooltip-max-width` | `20rem` | 气泡最大宽度 |
| `--tooltip-duration` | `0.2s` | 过渡持续时间 |
| `--tooltip-easing` | `ease` | 过渡时间函数 |
| `--tooltip-scale` | `1` | 气泡缩放比例 |
| `--tooltip-origin` | `center` | 变换原点 |
| `--tooltip-x` | `0` | 水平偏移 |
| `--tooltip-y` | `0` | 垂直偏移 |
| `--tooltip-start-scale` | `--tooltip-scale` | 初始缩放比例 |
| `--tooltip-end-scale` | `--tooltip-scale` | 可见时缩放比例 |
| `--tooltip-start-x` | `--tooltip-x` | 初始水平偏移 |
| `--tooltip-end-x` | `--tooltip-x` | 可见时水平偏移 |
| `--tooltip-start-y` | `--tooltip-y` | 初始垂直偏移 |
| `--tooltip-end-y` | `--tooltip-y` | 可见时垂直偏移 |

示例：

```css
.tooltip--custom {
  --tooltip-bg: #2563eb;
  --tooltip-color: #ffffff;
  --tooltip-border-radius: 8px;
  --tooltip-padding: 8px 12px;
  --tooltip-box-shadow: 0 4px 12px rgb(0 0 0 / 15%);
  --tooltip-gap: 0.5rem;
}
```

## 精简版本

如果您不想使用 CSS 变量并追求尽可能小的体积，本项目提供了精简版本（`compact.css` / `compact.min.css`），保留了基于 CSS Anchor Positioning 的自动定位以及针对不支持浏览器的回退方案。

鉴于其体积极小（未压缩约 1 KB，压缩后约 800 B），建议直接将 [compact.css](compact.css) 的内容复制并粘贴到您的项目样式表中，而不是作为外部依赖引入。这样您无需通过变量即可直接在 CSS 中完全自定义提示框的样式。

如果您仍想从包中直接引入：

```js
import '@zkreations/tooltips/compact.min.css';
```

## 设计上不含箭头

v5 不包含伪元素箭头（`::after`）。`flip-block` 与 `flip-inline` 改变气泡位置时，无法在所有浏览器中一致地将方向变化传达给伪元素边框，这会产生视觉错误。省略箭头可避免这些错误并保持样式表更小。

## 浏览器兼容性

- 支持 CSS Anchor Positioning 的浏览器使用 `@supports (position-area: block-start)` 实现动态定位和自动切换。
- 不支持的浏览器收到静态回退：顶部居中的绝对定位气泡。
- 当前支持情况：[Can I Use — CSS Anchor Positioning](https://caniuse.com/css-anchor-positioning)。

## 从 v4 迁移到 v5

| v4 | v5 |
| --- | --- |
| `[data-tts]` | `.tooltip` |
| `data-tts-visible` | `data-tooltip-visible` |
| `[data-tts="down"]` | `--tooltip-area: block-end;` |
| `[data-tts="left"]` | `--tooltip-area: inline-start;` |
| `[data-tts="right"]` | `--tooltip-area: inline-end;` |
| `--tts-*` | `--tooltip-*` |
| `tooltips.min.css` | `index.min.css` |

## 支持

如果你想帮助维持这个项目的更新，可以[请我喝咖啡](https://ko-fi.com/zkreations)。

## 许可证

MIT 许可证
