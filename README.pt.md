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
  position-area: var(--tt-area, block-start);
  position-try-fallbacks: var(--tt-fallbacks, flip-block, flip-inline);
}
```

Para definir uma posição personalizada, sobrescrever `--tt-area`:

```css
.tooltip--right  { --tt-area: inline-end; }
.tooltip--left   { --tt-area: inline-start; }
.tooltip--bottom { --tt-area: block-end; }
```

Para forçar uma posição sem alternância automática:

```css
.tooltip--fixed-right {
  --tt-area: inline-end;
  --tt-fallbacks: none;
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
| `--tt-area` | `block-start` | Área de posição relativa à âncora |
| `--tt-fallbacks` | `flip-block, flip-inline` | Posições de fallback se recortado |
| `--tt-gap` | `0.5rem` | Espaçamento entre âncora e tooltip |
| `--tt-bg` | `rgb(0 0 0 / 90%)` | Cor de fundo |
| `--tt-color` | `#fff` | Cor do texto |
| `--tt-size` | `0.875rem` | Tamanho da fonte |
| `--tt-padding` | `0.5em 0.75em` | Padding da bolha |
| `--tt-radius` | `0.25em` | Raio da borda |
| `--tt-shadow` | `none` | Sombra da bolha |
| `--tt-max-width` | `20rem` | Largura máxima da bolha |
| `--tt-z-index` | `10` | Ordem de empilhamento (z-index) |
| `--tt-duration` | `0.2s` | Duração da transição |
| `--tt-ease` | `ease` | Função de temporização da transição |
| `--tt-start` | `none` | Transformação em repouso (ex. `scale(0.85)`, `translateY(6px)`) |
| `--tt-end` | `none` | Transformação no estado visível |

Exemplo:

```css
.tooltip--custom {
  --tt-bg: #2563eb;
  --tt-color: #ffffff;
  --tt-radius: 8px;
  --tt-padding: 8px 12px;
  --tt-shadow: 0 4px 12px rgb(0 0 0 / 15%);
  --tt-gap: 0.5rem;
}
```

## Versão compacta

Se você prefere não utilizar variáveis CSS e busca o menor tamanho possível, o proyecto inclui uma variante compacta (`compact.css` / `compact.min.css`) que mantém o posicionamento automático via CSS Anchor Positioning e o fallback para navegadores sem suporte.

Devido ao seu tamanho reduzido (~1 KB sem minificar / ~800 B minificado), é recomendável copiar diretamente o conteúdo de [compact.css](compact.css) para a folha de estilos do seu projeto em vez de carregá-lo como dependência externa. Dessa forma, você pode editar e personalizar qualquer aspecto visual do tooltip diretamente no CSS, sem recorrer a variáveis.

Se ainda assim preferir importá-lo pelo pacote:

```js
import '@zkreations/tooltips/compact.min.css';
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
| `[data-tts="down"]` | `--tt-area: block-end;` |
| `[data-tts="left"]` | `--tt-area: inline-start;` |
| `[data-tts="right"]` | `--tt-area: inline-end;` |
| `--tts-*` | `--tt-*` |
| `tooltips.min.css` | `index.min.css` |

## Suporte

Se quiser ajudar a manter este projeto atualizado, pode [me pagar um café](https://ko-fi.com/zkreations).

## Licença

Licença MIT
