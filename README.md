<div align="center">
  <img width='100' src="https://raw.githubusercontent.com/zkreations/tooltips/master/.github/tooltips.svg?sanitize=true" align="center" />

  # Tooltips.css

  <p>A lightweight and powerful solution that doesn't rely on JavaScript and compresses to just 0.7kb (<a href="https://www.multiutil.com/text-to-brotli-compress/">Brotli</a>). Easy to customize and implement, with no impact on performance.</p>

  <a href="https://www.jsdelivr.com/package/npm/@zkreations/tooltips">
    <img src="https://img.shields.io/jsdelivr/npm/hm/@zkreations/tooltips?color=68D391&style=for-the-badge"/>
  </a>
  <a href="https://www.npmjs.com/package/@zkreations/tooltips">
    <img src="https://img.shields.io/npm/v/@zkreations/tooltips?color=4FD1C5&style=for-the-badge"/>
  </a>

  <p><a href="https://zkreations.github.io/tooltips/"><strong> Live Demo &rarr;</strong></a></p>
</div>

## Installation

### npm

```
npm i @zkreations/tooltips
```

### cdn

```html
<link href="https://cdn.jsdelivr.net/npm/@zkreations/tooltips@4/tooltips.min.css" rel="stylesheet"/>
```

## How to use

Add the `data-tts` and `aria-label` attributes to an html element:

```html
<span data-tts aria-label="Hello world!">Tooltip</span>
```

### Positioning

If no orientation is specified, the default value (up) will be used:

```html
<span data-tts="up" aria-label="Up">Top</span>
<span data-tts="left" aria-label="Left">Left</span>
<span data-tts="right" aria-label="Right">Right</span>
<span data-tts="down" aria-label="Down">Bottom</span>
```

The "**up**" and "**down**" orientations can be combined with "**left**" and "**right**":

```html
<span data-tts="up-left" aria-label="Up Left">Up Left</span>
<span data-tts="up-right" aria-label="Up Right">Up Right</span>
<span data-tts="down-left" aria-label="Down Left">Down Left</span>
<span data-tts="down-right" aria-label="Down Right">Down Right</span>
```

### Animations

Animations can be created using **CSS variables** that affect the initial state:

| Variable                | Default  | Description
| ----------------------- | -------- | ------------
| `--tts-start-scale`     | `1`      | Initial scale
| `--tts-end-scale`       | `1`      | Final scale
| `--tts-start-translate` | `0px`    | Initial position
| `--tts-end-translate`   | `0px`    | Final position

With these variables, you can create animations, for example:

```css
.tts-slideIn {
  --tts-start-translate: -1rem;
}
.tts-slideOut {
  --tts-start-translate: 1rem;
}
.tts-zoomIn {
  --tts-start-scale: .9;
}
.tts-zoomOut {
  --tts-start-scale: 1.1;
}
```

Now just add the classes to your animations:

```html
<span data-tts class="tts-slideIn" aria-label="Slide In">SlideIn</span>
<span data-tts class="tts-slideOut" aria-label="Slide Out">SlideOut</span>
<span data-tts class="tts-zoomIn" aria-label="Zoom In">ZoomIn</span>
<span data-tts class="tts-zoomOut" aria-label="Zoom Out">ZoomOut</span>
```

You can also define a **default animation** for all tooltips without using classes:

```css
[data-tts] {
  --tts-start-translate: 1rem;
  --tts-start-scale: .75;
}
```

### Show programmable tooltip

Add the `data-tts-visible` class to display the tooltip at any time without the need for user interaction with the element. You can easily add this attribute using JavaScript.

```html
<span data-tts data-tts-visible aria-label="Programmatically Visible">Hello world</span>
```

## Customize

Define new values for the tooltip's CSS variables to change its appearance. The available design variables are:

| Variable              | Default              | Description
| --------------------- | -------------------- | -------------
| `--tts-background`    | rgb(0 0 0 / 90%)     | Background color
| `--tts-arrow`         | 6px                  | Arrow size
| `--tts-arrow-offset`  | 6px                  | Arrow offset (only for combined orientation)
| `--tts-duration`      | 0.3s                 | Animation duration
| `--tts-font-size`     | 14px                 | Font size
| `--tts-font-family`   | Roboto, sans-serif   | Font family
| `--tts-color`         | #fff                 | Font color
| `--tts-padding`       | 0.5em 0.75em         | Padding
| `--tts-border-radius` | 0.25em               | Border radius

Variables allow you to create new themes that you can apply with your own classes:

```css
.tts-custom {
  --tts-background: #607D8B;
  --tts-border-radius: 1em;
  --tts-duration: .5s;
}
```

You can also set **global styles** for all tooltips:

```css
[data-tts] {
  --tts-background: #607D8B;
  --tts-border-radius: 0px;
}
```

## Notes

Tooltips **do not work with self-closing tags**, for example, `<img/>` or `<input/>`. To fix this, create a container and initiate the tooltip inside it:

```html
<figure data-tts aria-label="I am an image">
  <img src="example.jpg"/>
</figure>
```

## Supporting

If you want to help me keep this and more related projects always up to date, you can [buy me a coffee](https://ko-fi.com/zkreations) ☕. I will be very grateful 👏.

## License

**tooltips.css** is licensed under the MIT License
