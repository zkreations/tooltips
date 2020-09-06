<div align="center">
  <img src="/static/tts-logo.svg?sanitize=true" width="200" alt="Canvas.xml Logo">
  <h1>Tooltips.css</h1>
  <p>Tiny and powerful tooltips with pure css ~ 0.8kb gzipped</p>
  
  <a href="https://www.jsdelivr.com/package/gh/zkreations/tooltips">
    <img src="https://img.shields.io/jsdelivr/gh/hm/zkreations/tooltips?color=D69E2E&style=for-the-badge"/>
  </a>
  <a href="https://github.com/zkreations/tooltips/releases/">
    <img src="https://img.shields.io/github/v/release/zkreations/tooltips?color=68D391&style=for-the-badge"/>
  </a>
  <a href="./LICENSE">
    <img src="https://img.shields.io/github/license/zkreations/tooltips?color=4FD1C5&style=for-the-badge"/>
  </a>
</div>

## Installation

### CDN

```html
<link href="//cdn.jsdelivr.net/gh/zkreations/tooltips@3/tooltips.min.css" rel="stylesheet">
```

### Manual
Descargue **tooltips.min.css** de este repositorio e incluya el archivo en su código HTML:

```html
<link href="tooltips.min.css" rel="stylesheet">
```

## Usage

### Default
Agregue clase ``tts`` y el atributo ``aria-label`` a un elemento html:

```html
<span class="tts" aria-label="Hola mundo!">Tooltip</span>
```
### Positioning

Para cambiar la dirección agregue dos puntos seguido de una posición:

```html
<span class="tts" aria-label="Hacia arriba por defecto">Tooltip</span>
<span class="tts:left" aria-label="Hacia la izquierda">Tooltip</span>
<span class="tts:right" aria-label="Hacia la derecha">Tooltip</span>
<span class="tts:down" aria-label="Hacia la abajo">Tooltip</span>
```

### Animations

Escoja entre ``tts-slideIn``, ``tts-slideOut``, ``tts-zoomIn`` y ``tts-zoomOut`` ejemplo:

```html
<span class="tts" aria-label="Fade (defualt)">Tooltip</span>
<span class="tts tts-slideIn" aria-label="Slide In">Tooltip</span>
<span class="tts tts-slideOut" aria-label="Slide Out">Tooltip</span>
<span class="tts tts-zoomIn" aria-label="Zoom In">Tooltip</span>
<span class="tts tts-zoomOut" aria-label="Zoom Out">Tooltip</span>
```

### Always Visible
Agregue la clase ``tts-visible`` para que el tooltip se muestre siempre visible:

```html
<span class="tts tts-visible" aria-label="Siempre visible">Tooltip</span>
```

### Line Break
Por defecto el tooltip contiene la propiedad ``nowrap``. Agregue la clase ``tts-wrap`` para respetar los saltos de linea:

```html
<span class="tts tts-wrap" aria-label="Los saltos de linea se respetan">Tooltip</span>
```

### Is it a block?
Por defecto se aplica la propiedad display ``inline-block`` a todos los elementos con tooltip, si no quiere que esto ocurra, agregue la clase ``tts-block`` para retirar las propieades ``inline-block`` del elemento:

```html
<div class="tts tts-block" aria-label="Adiós inline-block">Tooltip</div>
```

## License

**tooltips.css** is licensed under the MIT License

