<p align="center">
  <img src="https://raw.githubusercontent.com/zkreations/tooltips/master/.github/tooltips.svg?sanitize=true" width="128" alt="tooltips" />
  <h1 align="center">Tooltips</h1>
  <p align="center">
    <a href="README.md">English</a> ·
    <a href="README.es.md">Español</a> ·
    <a href="README.fr.md">Français</a> ·
    <strong>Português</strong> ·
    <a href="README.zh.md">中文</a> ·
    <a href="README.ja.md">日本語</a>
    —
    <a href="https://zkreations.github.io/tooltips/">Demo</a>
  </p>
</p>

<p align="center">Biblioteca de tooltips em CSS puro. Sem JavaScript, sem dependências, sem configuração, moderna com fallback para navegadores sem suporte, ~0,5 KB minificado (Brotli)</p>

<p align="center">
  <a href="https://www.jsdelivr.com/package/npm/@zkreations/tooltips"><img src="https://img.shields.io/jsdelivr/npm/hm/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=f97316" alt="jsdelivr"></a>
  <a href="https://www.npmjs.com/package/@zkreations/tooltips"><img src="https://img.shields.io/npm/v/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=a855f7" alt="npmjs"></a>
  <a href="https://www.npmjs.com/package/@zkreations/tooltips"><img src="https://img.shields.io/npm/l/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=6366f1" alt="license"></a>
</p>

## Por que esta biblioteca em vez de uma baseada em JavaScript

A maioria das bibliotecas de tooltips requer JavaScript para calcular posições, anexar event listeners e gerenciar o estado de visibilidade. Esta biblioteca não faz nada disso — todo o comportamento é declarado em CSS.

## Características

* **CSS puro.** Sem JavaScript, dependências ou configuração.
* **Posicionamento nativo.** Usa CSS Anchor Positioning para calcular a posição e alternar automaticamente de lado quando o espaço é insuficiente.
* **Código mínimo.** A folha de estilos contém apenas as regras necessárias para o comportamento base; não inclui classes para posições, estilos ou animações que talvez não sejam usadas.
* **Configuração via CSS.** Cada tooltip pode definir sua posição, aparência e animação através de propriedades CSS personalizadas, conforme as necessidades do projeto.
* **Sem layout shift.** O posicionamento ocorre durante o cálculo do layout pelo navegador, sem medir o DOM após a renderização.
* **Acessível.** Usa `aria-label` como conteúdo e exibe tooltips ao receber `:focus`.
* **Fallback automático.** Navegadores sem CSS Anchor Positioning usam uma posição absoluta centralizada no topo.

> [!IMPORTANT]
> CSS Anchor Positioning é uma funcionalidade relativamente recente. Os navegadores que não a suportam recebem um fallback previsível (bolha centralizada no topo, posição absoluta) em vez de posicionamento dinâmico.

## Instalação

### npm

```bash
npm i @zkreations/tooltips
```

### Frameworks e bundlers

O pacote exporta seu CSS minificado como entrada de estilos padrão:

```js
import '@zkreations/tooltips';
```

Importar uma única vez no ponto de entrada da aplicação:

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

O mesmo import funciona com Vite, Nuxt, SvelteKit e outros bundlers que suportem imports de CSS de pacotes. Se um bundler não resolver a entrada de estilos do pacote, importar o arquivo diretamente:

```js
import '@zkreations/tooltips/index.min.css';
```

Não importar ambos os caminhos — contêm a mesma folha de estilos.

### Sass

Usar a entrada Sass apenas quando o projeto precisar compilar o código-fonte:

```scss
@use '@zkreations/tooltips/scss/tooltip';
```

Nesse caso, não importar também o CSS do pacote. A maioria dos projetos deve usar a entrada CSS compilada.

### CDN

```html
<link href="https://cdn.jsdelivr.net/npm/@zkreations/tooltips@5/index.min.css" rel="stylesheet"/>
```

## Uso

Adicionar a classe `.tooltip` e o atributo `aria-label` a qualquer elemento HTML:

```html
<button type="button" class="tooltip" aria-label="Olá mundo!">
  Passe o cursor ou foque em mim
</button>
```

### Posicionamento

Os tooltips aparecem acima (`block-start`) por padrão e alternam automaticamente (`flip-block, flip-inline`) quando o espaço é insuficiente:

```css
.tooltip::before {
  position-area: var(--tooltip-area, block-start);
  position-try-fallbacks: flip-block, flip-inline;
}
```

Para definir uma posição personalizada, sobrescrever `--tooltip-area`:

```css
.tooltip--right  { --tooltip-area: inline-end; }
.tooltip--left   { --tooltip-area: inline-start; }
.tooltip--bottom { --tooltip-area: block-end; }
```

Para forçar uma posição sem alternância automática:

```css
.tooltip--fixed-right {
  --tooltip-area: inline-end;
  position-try-fallbacks: none;
}
```

### Visibilidade programática

Para exibir um tooltip sem hover ou foco, adicionar `data-tooltip-visible`:

```html
<button type="button" class="tooltip" aria-label="Notificação ativa" data-tooltip-visible>
  Notificações
</button>
```

## Personalização

Sobrescrever as propriedades CSS para ajustar a aparência:

| Variável | Valor padrão | Descrição |
| --- | --- | --- |
| `--tooltip-area` | `block-start` | Área de posição relativa à âncora |
| `--tooltip-gap` | `0.5rem` | Espaçamento entre âncora e tooltip |
| `--tooltip-bg` | `rgb(0 0 0 / 90%)` | Cor de fundo |
| `--tooltip-color` | `#fff` | Cor do texto |
| `--tooltip-font-size` | `0.875rem` | Tamanho da fonte |
| `--tooltip-font-family` | `inherit` | Família tipográfica |
| `--tooltip-line-height` | `1.5` | Altura da linha |
| `--tooltip-padding` | `0.5em 0.75em` | Padding da bolha |
| `--tooltip-border-radius` | `0.25em` | Raio da borda |
| `--tooltip-max-width` | `20rem` | Largura máxima da bolha |
| `--tooltip-duration` | `0.2s` | Duração da transição |
| `--tooltip-easing` | `ease` | Função de temporização da transição |
| `--tooltip-scale` | `1` | Escala da bolha |
| `--tooltip-origin` | `center` | Origem da transformação |
| `--tooltip-x` | `0` | Deslocamento horizontal |
| `--tooltip-y` | `0` | Deslocamento vertical |
| `--tooltip-start-scale` | `--tooltip-scale` | Escala inicial |
| `--tooltip-end-scale` | `--tooltip-scale` | Escala visível |
| `--tooltip-start-x` | `--tooltip-x` | Deslocamento horizontal inicial |
| `--tooltip-end-x` | `--tooltip-x` | Deslocamento horizontal visível |
| `--tooltip-start-y` | `--tooltip-y` | Deslocamento vertical inicial |
| `--tooltip-end-y` | `--tooltip-y` | Deslocamento vertical visível |

Exemplo:

```css
.tooltip--custom {
  --tooltip-bg: #2563eb;
  --tooltip-color: #ffffff;
  --tooltip-border-radius: 8px;
  --tooltip-padding: 8px 12px;
  --tooltip-gap: 0.5rem;
}
```

## Sem seta, por design

A v5 não inclui uma seta como pseudo-elemento (`::after`). `flip-block` e `flip-inline` alteram o posicionamento da bolha sem comunicar as mudanças de orientação às bordas dos pseudo-elementos de forma consistente entre os navegadores, o que produz bugs visuais. Omitir a seta evita esses bugs e mantém a folha de estilos menor.

## Compatibilidade com navegadores

- Os navegadores que suportam CSS Anchor Positioning usam `@supports (position-area: block-start)` para posicionamento dinâmico e alternância automática.
- Os navegadores sem suporte recebem um fallback estático: uma bolha centralizada no topo em posição absoluta.
- Suporte atual: [Can I Use — CSS Anchor Positioning](https://caniuse.com/css-anchor-positioning).

## Migração de v4 para v5

| v4 | v5 |
| --- | --- |
| `[data-tts]` | `.tooltip` |
| `data-tts-visible` | `data-tooltip-visible` |
| `[data-tts="down"]` | `--tooltip-area: block-end;` |
| `[data-tts="left"]` | `--tooltip-area: inline-start;` |
| `[data-tts="right"]` | `--tooltip-area: inline-end;` |
| `--tts-*` | `--tooltip-*` |
| `tooltips.min.css` | `index.min.css` |

## Suporte

Se quiser ajudar a manter este projeto atualizado, pode [me pagar um café](https://ko-fi.com/zkreations).

## Licença

Licença MIT
