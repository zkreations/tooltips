<div align="center">
  <img src=".github/tooltips.svg?sanitize=true" width="120" alt="tts-tooltips">
  <h1>Tooltips.css</h1>
  <p>Ligero y poderoso tooltips sin javascript ~ 0.9kb gzipped</p>
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

## Instalar

### CDN

```html
<link href="https://cdn.jsdelivr.net/gh/zkreations/tooltips@4/tooltips.min.css" rel="stylesheet"/>
```

## Modo de uso

Agrega los atributos `data-tts` y `aria-label` a un elemento html:

```html
<span data-tts aria-label="Hola mundo!">Tooltip</span>
```

### Orientación

Si no se especifica una orientación se usara el valor por defecto (up):

```html
<span data-tts="up" aria-label="Arriba">Top</span>
<span data-tts="left" aria-label="Izquierda">Left</span>
<span data-tts="right" aria-label="Derecha">Right</span>
<span data-tts="down" aria-label="Abajo">Bottom</span>
```

Las orientaciones **"up"** y **"down"** se pueden combinar con **"left"** y **"right"**:

```html
<span data-tts="up-left" aria-label="Inicio">Inicio</span>
<span data-tts="up-right" aria-label="Esquina">Esquina</span>
<span data-tts="down-left" aria-label="Inferior">Inferior</span>
<span data-tts="down-right" aria-label="Final">Final</span>
```

### Animaciones

Las animaciones pueden crearse con **variables css** que afectan al estado inicial:

| Variable                |  Default | Descripción
| ----------------------- | -------- | ------------
| `--tts-start-scale`     | `1`      | Escala inicial
| `--tts-end-scale`       | `1`      | Escala final
| `--tts-start-translate` | `0px`    | Posición inicial 
| `--tts-end-translate`   | `0px`    | Posición Final 

Con ellas podemos recrear las animaciones, por ejemplo:

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

Ahora solo agrega las clases de tus animaciones:

```html
<span data-tts class="tts-slideIn" aria-label="Slide In">SlideIn</span>
<span data-tts class="tts-slideOut" aria-label="Slide Out">SlideOut</span>
<span data-tts class="tts-zoomIn" aria-label="Zoom In">ZoomIn</span>
<span data-tts class="tts-zoomOut" aria-label="Zoom Out">ZoomOut</span>
```

También puedes definir una **animación por defecto** para todos los tooltips, sin usar clases:

```css
[data-tts] {
  --tts-start-translate: 1rem;
  --tts-start-scale: .75;
}
```

### Mostrar tooltip programable

Agrega el atributo clase `data-tts-visible` para mostrar en cualquier momento el tooltip sin la necesidad de que el usuario interactue con el elemento. Puedes agregar fácilmente este atributo utilizando Javascript.

```html
<span data-tts data-tts-visible aria-label="Visible programado">Hola mundo</span>
```

## Personalizar

Define nuevos valores para las variables css del tooltip para cambiar su aspecto. Las variables de diseño disponibles son:

| Variable              | Default              | Descripción
| --------------------- | -------------------- | -------------
| `--tts-background`    | rgb(0 0 0 / 90%)     | Color de fondo
| `--tts-arrow`         | 6px                  | Tamaño del indicador
| `--tts-arrow-offset`  | 6px                  | Espacios laterales (solo para orientación combinada)
| `--tts-duration`      | 0.3s                 | Duración de animación
| `--tts-font-size`     | 14px                 | Tamaño de fuente
| `--tts-font-family`   | Roboto, sans-serif   | Estilo de fuente
| `--tts-color`         | #fff                 | Color de textos
| `--tts-padding`       | 0.5em 0.75em         | Espacio de relleno 
| `--tts-border-radius` | 0.25em               | Bordes redondeados

Las variables permiten crear nuevos temas que puedes aplicar con tus propias clases:

```css
.tts-custom {
  --tts-background: #607D8B;
  --tts-border-radius: 1em;
  --tts-duration: .5s;
}
```

También puedes establecer **estilos globales** para todos los tooltips:

```css
[data-tts] {
  --tts-background: #607D8B;
  --tts-border-radius: 0px;
}
```

## Observaciones

Los tooltips **no funcionan con etiquetas de auto cierre**, por ejemplo `<img/>` o `<input/>`. Para solucionarlo, crea un contenedor e inicia el globo en él:

```html
<figure data-tts aria-label="Soy una imagen">
  <img src="example.jpg"/>
</figure>
```

## License

**tooltips.css** is licensed under the MIT License
