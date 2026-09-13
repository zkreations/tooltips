<p align="center">
  <img src="https://raw.githubusercontent.com/zkreations/tooltips/master/.github/tooltips.svg?sanitize=true" width="128" alt="tooltips" />
  <h1 align="center">Tooltips</h1>
  <p align="center">
    <a href="README.md">English</a> ·
    <strong>Español</strong> ·
    <a href="README.fr.md">Français</a> ·
    <a href="README.pt.md">Português</a> ·
    <a href="README.zh.md">中文</a> ·
    <a href="README.ja.md">日本語</a>
    —
    <a href="https://zkreations.github.io/tooltips/">Demo</a>
  </p>
</p>

<p align="center">Librería de tooltips en CSS puro. Sin JavaScript, sin dependencias, sin configuración, moderno con fallback para navegadores que no soporten, ~0,5 kb minimizado (Brotli)</p>

<p align="center">
  <a href="https://www.jsdelivr.com/package/npm/@zkreations/tooltips"><img src="https://img.shields.io/jsdelivr/npm/hm/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=f97316" alt="jsdelivr"></a>
  <a href="https://www.npmjs.com/package/@zkreations/tooltips"><img src="https://img.shields.io/npm/v/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=a855f7" alt="npmjs"></a>
  <a href="https://www.npmjs.com/package/@zkreations/tooltips"><img src="https://img.shields.io/npm/l/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=6366f1" alt="license"></a>
</p>

## Por qué esta librería en lugar de una basada en JavaScript

La mayoría de las librerías de tooltips requieren JavaScript para calcular posiciones, adjuntar event listeners y gestionar el estado de visibilidad. Esta librería no hace nada de eso — todo el comportamiento está declarado en CSS.

## Características

* **CSS puro.** Sin JavaScript, dependencias ni configuración.
* **Posicionamiento nativo.** Usa CSS Anchor Positioning para calcular la posición y cambiar automáticamente de lado cuando no hay espacio.
* **Código mínimo.** La hoja de estilos contiene solo las reglas necesarias para el comportamiento base; no incluye clases para posiciones, estilos o animaciones que quizá no uses.
* **Configuración mediante CSS.** Cada tooltip puede definir su posición, apariencia y animación mediante propiedades CSS personalizadas, según las necesidades del proyecto.
* **Sin layout shift.** El posicionamiento ocurre durante el cálculo del layout del navegador, sin medir el DOM después del renderizado.
* **Accesible.** Usa `aria-label` como contenido y muestra los tooltips al recibir `:focus`.
* **Fallback automático.** Los navegadores sin CSS Anchor Positioning usan una posición absoluta superior y centrada.

> [!IMPORTANT]
> CSS Anchor Positioning es una funcionalidad relativamente reciente. Los navegadores que no la soportan reciben un fallback predecible (burbuja superior centrada, posición absoluta) en lugar de posicionamiento dinámico.

## Instalación

### npm

```bash
npm i @zkreations/tooltips
```

### Frameworks y bundlers

El paquete exporta su CSS minificado como entrada de estilos por defecto:

```js
import '@zkreations/tooltips';
```

Importarlo una sola vez en el punto de entrada de la aplicación:

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

La misma importación funciona con Vite, Nuxt, SvelteKit y otros bundlers que soporten importaciones de CSS desde paquetes. Si el bundler no resuelve la entrada de estilos del paquete, importar el archivo directamente:

```js
import '@zkreations/tooltips/index.min.css';
```

No importar ambas rutas — contienen la misma hoja de estilos.

### Sass

Usar la entrada Sass solo cuando el proyecto necesite compilar el código fuente:

```scss
@use '@zkreations/tooltips/scss/tooltip';
```

En ese caso, no importar también el CSS del paquete. La mayoría de los proyectos deben usar la entrada CSS compilada.

### CDN

```html
<link href="https://cdn.jsdelivr.net/npm/@zkreations/tooltips@5/index.min.css" rel="stylesheet"/>
```

## Uso

Añadir la clase `.tooltip` y el atributo `aria-label` a cualquier elemento HTML:

```html
<button type="button" class="tooltip" aria-label="¡Hola mundo!">
  Pasa el cursor o enfócame
</button>
```

### Posicionamiento

Los tooltips aparecen arriba (`block-start`) por defecto y se desplazan automáticamente al lado opuesto (`flip-block`) cuando el espacio es insuficiente:

```css
.tooltip::before {
  position-area: var(--tooltip-area, block-start);
  position-try-fallbacks: var(--tooltip-fallbacks, flip-block);
}
```

Para definir una posición personalizada, sobreescribir `--tooltip-area`:

```css
.tooltip--right  { --tooltip-area: inline-end; }
.tooltip--left   { --tooltip-area: inline-start; }
.tooltip--bottom { --tooltip-area: block-end; }
```

Para forzar una posición sin desplazamiento automático:

```css
.tooltip--fixed-right {
  --tooltip-area: inline-end;
  --tooltip-fallbacks: none;
}
```

### Visibilidad programática

Para mostrar un tooltip sin hover ni foco, añadir `data-tooltip-visible`:

```html
<button type="button" class="tooltip" aria-label="Notificación activa" data-tooltip-visible>
  Notificaciones
</button>
```

## Personalización

Sobreescribir las propiedades CSS para ajustar la apariencia:

| Variable | Valor por defecto | Descripción |
| --- | --- | --- |
| `--tooltip-area` | `block-start` | Área de posición relativa al ancla |
| `--tooltip-fallbacks` | `flip-block` | Posiciones de fallback si se recorta |
| `--tooltip-gap` | `0.25rem` | Separación entre el ancla y el tooltip |
| `--tooltip-bg` | `rgb(0 0 0 / 90%)` | Color de fondo |
| `--tooltip-color` | `#fff` | Color del texto |
| `--tooltip-font-size` | `0.875rem` | Tamaño de fuente |
| `--tooltip-font-family` | `inherit` | Familia tipográfica |
| `--tooltip-line-height` | `1.5` | Altura de línea |
| `--tooltip-padding` | `0.5em 0.75em` | Padding de la burbuja |
| `--tooltip-border-radius` | `0.25em` | Radio de borde |
| `--tooltip-max-width` | `20rem` | Ancho máximo de la burbuja |
| `--tooltip-duration` | `0.2s` | Duración de la transición |
| `--tooltip-easing` | `ease` | Función de temporización de la transición |
| `--tooltip-scale` | `1` | Escala de la burbuja |
| `--tooltip-x` | `0` | Desplazamiento horizontal |
| `--tooltip-y` | `0` | Desplazamiento vertical |
| `--tooltip-start-scale` | `--tooltip-scale` | Escala inicial |
| `--tooltip-end-scale` | `--tooltip-scale` | Escala visible |
| `--tooltip-start-x` | `--tooltip-x` | Desplazamiento horizontal inicial |
| `--tooltip-end-x` | `--tooltip-x` | Desplazamiento horizontal visible |
| `--tooltip-start-y` | `--tooltip-y` | Desplazamiento vertical inicial |
| `--tooltip-end-y` | `--tooltip-y` | Desplazamiento vertical visible |

Ejemplo:

```css
.tooltip--custom {
  --tooltip-bg: #2563eb;
  --tooltip-color: #ffffff;
  --tooltip-border-radius: 8px;
  --tooltip-padding: 8px 12px;
  --tooltip-gap: 0.5rem;
}
```

## Sin flecha, por diseño

La v5 no incluye una flecha como pseudo-elemento (`::after`). `flip-block` cambia la posición de la burbuja sin comunicar el cambio de orientación a los bordes de pseudo-elementos de forma consistente en todos los navegadores, lo que produce errores visuales. Omitir la flecha evita esos errores y mantiene la hoja de estilos más pequeña.

## Compatibilidad con navegadores

- Los navegadores que soportan CSS Anchor Positioning usan `@supports (position-area: block-start)` para el posicionamiento dinámico y el desplazamiento automático.
- Los navegadores sin soporte reciben un fallback estático: una burbuja superior centrada en posición absoluta.
- Soporte actual: [Can I Use — CSS Anchor Positioning](https://caniuse.com/css-anchor-positioning).

## Migración de v4 a v5

| v4 | v5 |
| --- | --- |
| `[data-tts]` | `.tooltip` |
| `data-tts-visible` | `data-tooltip-visible` |
| `[data-tts="down"]` | `--tooltip-area: block-end;` |
| `[data-tts="left"]` | `--tooltip-area: inline-start;` |
| `[data-tts="right"]` | `--tooltip-area: inline-end;` |
| `--tts-*` | `--tooltip-*` |
| `tooltips.min.css` | `index.min.css` |


## Soporte

Si quieres ayudar a mantener este proyecto actualizado, puedes [invitarme a un café](https://ko-fi.com/zkreations) ☕.

## Licencia

Licencia MIT
