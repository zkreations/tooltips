<p align="center">
  <img src="https://raw.githubusercontent.com/zkreations/tooltips/master/.github/tooltips.svg?sanitize=true" width="128" alt="tooltips" />
  <h1 align="center">Tooltips</h1>
  <p align="center">
    <strong>English</strong> ·
    <a href="README.es.md">Español</a> ·
    <a href="README.fr.md">Français</a> ·
    <a href="README.pt.md">Português</a> ·
    <a href="README.zh.md">中文</a> ·
    <a href="README.ja.md">日本語</a>
    —
    <a href="https://zkreations.github.io/tooltips/">Demo</a>
  </p>
</p>

<p align="center">CSS-only tooltip library. No JavaScript, no dependencies, no configuration, modern with fallback for unsupported browsers, ~0.5 KB minified (Brotli)</p>

<p align="center">
  <a href="https://www.jsdelivr.com/package/npm/@zkreations/tooltips"><img src="https://img.shields.io/jsdelivr/npm/hm/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=f97316" alt="jsdelivr"></a>
  <a href="https://www.npmjs.com/package/@zkreations/tooltips"><img src="https://img.shields.io/npm/v/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=a855f7" alt="npmjs"></a>
  <a href="https://www.npmjs.com/package/@zkreations/tooltips"><img src="https://img.shields.io/npm/l/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=6366f1" alt="license"></a>
</p>

## Why this instead of a JS-based tooltip library

Most tooltip libraries require JavaScript to calculate positions, attach event listeners, and manage visibility state. This library does none of that — all behavior is declared in CSS.

## Features

* **Pure CSS.** No JavaScript, dependencies, or configuration.
* **Native positioning.** Uses CSS Anchor Positioning to calculate position and automatically flip sides when space is limited.
* **Minimal code.** The stylesheet contains only the rules needed for base behavior; it does not include classes for positions, styles, or animations you may not use.
* **CSS-driven configuration.** Each tooltip can define its position, appearance, and animation through CSS custom properties, according to the project's needs.
* **No layout shift.** Positioning occurs during the browser's layout calculation, without measuring the DOM after render.
* **Accessible.** Uses `aria-label` as content and shows tooltips on `:focus`.
* **Automatic fallback.** Browsers without CSS Anchor Positioning use an absolute top-centered position.

> [!IMPORTANT]
> CSS Anchor Positioning is a relatively recent browser feature. Browsers that do not support it receive a predictable fallback (centered, absolute top bubble) rather than dynamic placement.

## Installation

### npm

```bash
npm i @zkreations/tooltips
```

### Frameworks and bundlers

The package exports its minified CSS as the default style entry:

```js
import '@zkreations/tooltips';
```

Import it once in the application entrypoint:

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

The same import works with Vite, Nuxt, SvelteKit, and other bundlers that support CSS package imports. If a bundler does not resolve the package style entry, import the file explicitly:

```js
import '@zkreations/tooltips/index.min.css';
```

Do not import both paths — they contain the same stylesheet.

### Sass

Use the Sass entry only when the project needs to compile the source itself:

```scss
@use '@zkreations/tooltips/scss/tooltip';
```

Do not also import the package CSS in that case. Most projects should use the compiled CSS entry instead.

### CDN

```html
<link href="https://cdn.jsdelivr.net/npm/@zkreations/tooltips@5/index.min.css" rel="stylesheet"/>
```

## Usage

Add the `.tooltip` class and the `aria-label` attribute to any HTML element:

```html
<button type="button" class="tooltip" aria-label="Hello world!">
  Hover or focus me
</button>
```

### Positioning

Tooltips appear at the top (`block-start`) by default and flip automatically (`flip-block, flip-inline`) when space is limited:

```css
.tooltip::before {
  position-area: var(--tooltip-area, block-start);
  position-try-fallbacks: var(--tooltip-fallbacks, flip-block, flip-inline);
}
```

To set a custom position, override `--tooltip-area`:

```css
.tooltip--right  { --tooltip-area: inline-end; }
.tooltip--left   { --tooltip-area: inline-start; }
.tooltip--bottom { --tooltip-area: block-end; }
```

To force a position without automatic flipping:

```css
.tooltip--fixed-right {
  --tooltip-area: inline-end;
  --tooltip-fallbacks: none;
}
```

### Programmatic visibility

To show a tooltip without hover or focus, add `data-tooltip-visible`:

```html
<button type="button" class="tooltip" aria-label="Active notification" data-tooltip-visible>
  Notifications
</button>
```

## Customization

Override CSS variables to adjust the appearance:

| Variable | Default | Description |
| --- | --- | --- |
| `--tooltip-area` | `block-start` | Position area relative to anchor |
| `--tooltip-fallbacks` | `flip-block, flip-inline` | Fallback positions if clipped |
| `--tooltip-gap` | `0.5rem` | Spacing between anchor and tooltip |
| `--tooltip-bg` | `rgb(0 0 0 / 90%)` | Background color |
| `--tooltip-color` | `#fff` | Text color |
| `--tooltip-font-size` | `0.875rem` | Font size |
| `--tooltip-font-family` | `inherit` | Font family |
| `--tooltip-line-height` | `1.5` | Line height |
| `--tooltip-padding` | `0.5em 0.75em` | Bubble padding |
| `--tooltip-border` | `none` | Border |
| `--tooltip-border-radius` | `0.25em` | Border radius |
| `--tooltip-box-shadow` | `none` | Box shadow |
| `--tooltip-max-width` | `20rem` | Maximum bubble width |
| `--tooltip-duration` | `0.2s` | Transition duration |
| `--tooltip-easing` | `ease` | Transition timing function |
| `--tooltip-scale` | `1` | Bubble scale |
| `--tooltip-origin` | `center` | Transform origin |
| `--tooltip-x` | `0` | Horizontal offset |
| `--tooltip-y` | `0` | Vertical offset |
| `--tooltip-start-scale` | `--tooltip-scale` | Initial scale |
| `--tooltip-end-scale` | `--tooltip-scale` | Visible scale |
| `--tooltip-start-x` | `--tooltip-x` | Initial horizontal offset |
| `--tooltip-end-x` | `--tooltip-x` | Visible horizontal offset |
| `--tooltip-start-y` | `--tooltip-y` | Initial vertical offset |
| `--tooltip-end-y` | `--tooltip-y` | Visible vertical offset |

Example:

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

## Compact version

If you prefer not to use CSS variables and want the smallest possible footprint, the project provides a compact variant (`compact.css` / `compact.min.css`) that retains automatic positioning via CSS Anchor Positioning alongside the fallback for unsupported browsers.

Given how small it is (~1 KB unminified / ~800 B minified), we recommend copying the contents of [compact.css](compact.css) directly into your project's stylesheet instead of adding it as an external dependency. This gives you direct and complete control over the tooltip styles in CSS without going through variables.

If you still prefer importing it from the package:

```js
import '@zkreations/tooltips/compact.min.css';
```

## No arrow by design

v5 does not include a pseudo-element arrow (`::after`). `flip-block` and `flip-inline` change bubble placement without communicating orientation changes to pseudo-element borders consistently across browsers, which produces visual bugs. Omitting the arrow avoids those bugs and keeps the stylesheet smaller.

## Browser compatibility

- Browsers supporting CSS Anchor Positioning use `@supports (position-area: block-start)` for dynamic placement and automatic flipping.
- Browsers without support receive a static fallback: a centered, absolute top bubble.
- Current support: [Can I Use — CSS Anchor Positioning](https://caniuse.com/css-anchor-positioning).

## Migration from v4 to v5

| v4 | v5 |
| --- | --- |
| `[data-tts]` | `.tooltip` |
| `data-tts-visible` | `data-tooltip-visible` |
| `[data-tts="down"]` | `--tooltip-area: block-end;` |
| `[data-tts="left"]` | `--tooltip-area: inline-start;` |
| `[data-tts="right"]` | `--tooltip-area: inline-end;` |
| `--tts-*` | `--tooltip-*` |
| `tooltips.min.css` | `index.min.css` |

## Support

If you want to help keep this project updated, you can [buy me a coffee](https://ko-fi.com/zkreations).

## License

MIT License
