<p align="center">
  <img src="https://raw.githubusercontent.com/zkreations/tooltips/master/.github/tooltips.svg?sanitize=true" width="128" alt="tooltips" />
  <h1 align="center">Tooltips</h1>
  <p align="center">
    <a href="README.md">English</a> ·
    <a href="README.es.md">Español</a> ·
    <strong>Français</strong> ·
    <a href="README.pt.md">Português</a> ·
    <a href="README.zh.md">中文</a> ·
    <a href="README.ja.md">日本語</a>
    —
    <a href="https://zkreations.github.io/tooltips/">Demo</a>
  </p>
</p>

<p align="center">Bibliothèque de tooltips en CSS pur. Sans JavaScript, sans dépendances, sans configuration, moderne avec fallback pour les navigateurs non compatibles, ~0,5 Ko minifié (Brotli)</p>

<p align="center">
  <a href="https://www.jsdelivr.com/package/npm/@zkreations/tooltips"><img src="https://img.shields.io/jsdelivr/npm/hm/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=f97316" alt="jsdelivr"></a>
  <a href="https://www.npmjs.com/package/@zkreations/tooltips"><img src="https://img.shields.io/npm/v/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=a855f7" alt="npmjs"></a>
  <a href="https://www.npmjs.com/package/@zkreations/tooltips"><img src="https://img.shields.io/npm/l/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=6366f1" alt="license"></a>
</p>

## Pourquoi cette bibliothèque plutôt qu'une basée sur JavaScript

La plupart des bibliothèques de tooltips nécessitent JavaScript pour calculer les positions, attacher des écouteurs d'événements et gérer l'état de visibilité. Cette bibliothèque ne fait rien de tout cela — tout le comportement est déclaré en CSS.

## Caractéristiques

* **CSS pur.** Sans JavaScript, dépendances ni configuration.
* **Positionnement natif.** Utilise CSS Anchor Positioning pour calculer la position et basculer automatiquement de côté lorsque l'espace est insuffisant.
* **Code minimal.** La feuille de styles ne contient que les règles nécessaires au comportement de base ; elle n'inclut pas de classes pour les positions, styles ou animations que vous n'utiliserez peut-être pas.
* **Configuration via CSS.** Chaque tooltip peut définir sa position, son apparence et son animation via des propriétés CSS personnalisées, selon les besoins du projet.
* **Sans layout shift.** Le positionnement s'effectue lors du calcul du layout par le navigateur, sans mesurer le DOM après le rendu.
* **Accessible.** Utilise `aria-label` comme contenu et affiche les tooltips au `:focus`.
* **Fallback automatique.** Les navigateurs sans CSS Anchor Positioning utilisent une position absolue centrée en haut.

> [!IMPORTANT]
> CSS Anchor Positioning est une fonctionnalité relativement récente. Les navigateurs qui ne la supportent pas reçoivent un fallback prévisible (bulle centrée en haut, position absolue) plutôt qu'un positionnement dynamique.

## Installation

### npm

```bash
npm i @zkreations/tooltips
```

### Frameworks et bundlers

Le package exporte son CSS minifié comme entrée de styles par défaut :

```js
import '@zkreations/tooltips';
```

L'importer une seule fois dans le point d'entrée de l'application :

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

Le même import fonctionne avec Vite, Nuxt, SvelteKit et autres bundlers supportant les imports CSS depuis des packages. Si un bundler ne résout pas l'entrée de styles du package, importer le fichier directement :

```js
import '@zkreations/tooltips/index.min.css';
```

Ne pas importer les deux chemins — ils contiennent la même feuille de styles.

### Sass

Utiliser l'entrée Sass uniquement lorsque le projet doit compiler le code source :

```scss
@use '@zkreations/tooltips/scss/tooltip';
```

Dans ce cas, ne pas importer également le CSS du package. La plupart des projets devraient utiliser l'entrée CSS compilée.

### CDN

```html
<link href="https://cdn.jsdelivr.net/npm/@zkreations/tooltips@5/index.min.css" rel="stylesheet"/>
```

## Utilisation

Ajouter la classe `.tooltip` et l'attribut `aria-label` à n'importe quel élément HTML :

```html
<button type="button" class="tooltip" aria-label="Bonjour le monde !">
  Survolez ou focalisez-moi
</button>
```

### Positionnement

Les tooltips apparaissent en haut (`block-start`) par défaut et basculent automatiquement (`flip-block, flip-inline`) lorsque l'espace est insuffisant :

```css
.tooltip::before {
  position-area: var(--tooltip-area, block-start);
  position-try-fallbacks: var(--tooltip-fallbacks, flip-block, flip-inline);
}
```

Pour définir une position personnalisée, surcharger `--tooltip-area` :

```css
.tooltip--right  { --tooltip-area: inline-end; }
.tooltip--left   { --tooltip-area: inline-start; }
.tooltip--bottom { --tooltip-area: block-end; }
```

Pour forcer une position sans basculement automatique :

```css
.tooltip--fixed-right {
  --tooltip-area: inline-end;
  --tooltip-fallbacks: none;
}
```

### Visibilité programmable

Pour afficher un tooltip sans survol ni focus, ajouter `data-tooltip-visible` :

```html
<button type="button" class="tooltip" aria-label="Notification active" data-tooltip-visible>
  Notifications
</button>
```

## Personnalisation

Surcharger les propriétés CSS pour ajuster l'apparence :

| Variable | Valeur par défaut | Description |
| --- | --- | --- |
| `--tooltip-area` | `block-start` | Zone de position relative à l'ancre |
| `--tooltip-fallbacks` | `flip-block, flip-inline` | Positions de fallback si rognée |
| `--tooltip-gap` | `0.5rem` | Espacement entre l'ancre et le tooltip |
| `--tooltip-bg` | `rgb(0 0 0 / 90%)` | Couleur de fond |
| `--tooltip-color` | `#fff` | Couleur du texte |
| `--tooltip-font-size` | `0.875rem` | Taille de police |
| `--tooltip-font-family` | `inherit` | Famille typographique |
| `--tooltip-line-height` | `1.5` | Hauteur de ligne |
| `--tooltip-padding` | `0.5em 0.75em` | Padding de la bulle |
| `--tooltip-border-radius` | `0.25em` | Rayon de bordure |
| `--tooltip-box-shadow` | `none` | Ombre de la bulle |
| `--tooltip-max-width` | `20rem` | Largeur maximale de la bulle |
| `--tooltip-duration` | `0.2s` | Durée de la transition |
| `--tooltip-easing` | `ease` | Fonction de temporisation |
| `--tooltip-scale` | `1` | Échelle de la bulle |
| `--tooltip-origin` | `center` | Origine de transformation |
| `--tooltip-x` | `0` | Décalage horizontal |
| `--tooltip-y` | `0` | Décalage vertical |
| `--tooltip-start-scale` | `--tooltip-scale` | Échelle initiale |
| `--tooltip-end-scale` | `--tooltip-scale` | Échelle visible |
| `--tooltip-start-x` | `--tooltip-x` | Décalage horizontal initial |
| `--tooltip-end-x` | `--tooltip-x` | Décalage horizontal visible |
| `--tooltip-start-y` | `--tooltip-y` | Décalage vertical initial |
| `--tooltip-end-y` | `--tooltip-y` | Décalage vertical visible |

Exemple :

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

## Version compacte

Si vous préférez ne pas utiliser de variables CSS et recherchez l'empreinte la plus réduite possible, le projet inclut une variante compacte (`compact.css` / `compact.min.css`) qui conserve le positionnement automatique via CSS Anchor Positioning ainsi que le fallback pour les navigateurs non compatibles.

En raison de sa très petite taille (~1 Ko non minifié / ~800 o minifié), il est recommandé de copier directement le contenu de [compact.css](compact.css) dans la feuille de styles de votre projet au lieu de l'importer comme dépendance externe. Cela vous permet d'éditer et de personnaliser directement l'intégralité des styles du tooltip en CSS sans passer par des variables.

Si vous préférez tout de même l'importer depuis le package :

```js
import '@zkreations/tooltips/compact.min.css';
```

## Sans flèche, par conception

La v5 n'inclut pas de flèche en pseudo-élément (`::after`). `flip-block` et `flip-inline` modifient le placement de la bulle sans communiquer les changements d'orientation aux bordures des pseudo-éléments de façon cohérente entre les navigateurs, ce qui produit des bugs visuels. Omettre la flèche évite ces bugs et réduit la taille de la feuille de styles.

## Compatibilité des navigateurs

- Les navigateurs supportant CSS Anchor Positioning utilisent `@supports (position-area: block-start)` pour le positionnement dynamique et le basculement automatique.
- Les navigateurs sans support reçoivent un fallback statique : une bulle centrée en haut en position absolue.
- Support actuel : [Can I Use — CSS Anchor Positioning](https://caniuse.com/css-anchor-positioning).

## Migration de v4 à v5

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

Si vous souhaitez aider à maintenir ce projet à jour, vous pouvez [m'offrir un café](https://ko-fi.com/zkreations).

## Licence

Licence MIT
