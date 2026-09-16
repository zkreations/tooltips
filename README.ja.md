<p align="center">
  <img src="https://raw.githubusercontent.com/zkreations/tooltips/master/.github/tooltips.svg?sanitize=true" width="128" alt="tooltips" />
  <h1 align="center">Tooltips</h1>
  <p align="center">
    <a href="README.md">English</a> ·
    <a href="README.es.md">Español</a> ·
    <a href="README.fr.md">Français</a> ·
    <a href="README.pt.md">Português</a> ·
    <a href="README.zh.md">中文</a> ·
    <strong>日本語</strong>
    —
    <a href="https://zkreations.github.io/tooltips/">Demo</a>
  </p>
</p>

<p align="center">純粋な CSS のツールチップライブラリ。JavaScript なし、依存関係なし、設定不要。未対応ブラウザへのフォールバック付き、圧縮後約 0.5 KB（Brotli）</p>

<p align="center">
  <a href="https://www.jsdelivr.com/package/npm/@zkreations/tooltips"><img src="https://img.shields.io/jsdelivr/npm/hm/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=f97316" alt="jsdelivr"></a>
  <a href="https://www.npmjs.com/package/@zkreations/tooltips"><img src="https://img.shields.io/npm/v/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=a855f7" alt="npmjs"></a>
  <a href="https://www.npmjs.com/package/@zkreations/tooltips"><img src="https://img.shields.io/npm/l/@zkreations/tooltips?style=for-the-badge&labelColor=030712&color=6366f1" alt="license"></a>
</p>

## JavaScript ベースのライブラリではなくこれを選ぶ理由

ほとんどのツールチップライブラリは、位置の計算、イベントリスナーの登録、表示状態の管理に JavaScript を必要とします。このライブラリはそのいずれも行いません——すべての動作は CSS で宣言されています。

## 特徴

* **純粋な CSS。** JavaScript、依存関係、設定は不要です。
* **ネイティブポジショニング。** CSS Anchor Positioning を使用して位置を計算し、スペースが不足した場合に自動的に反対側へ切り替えます。
* **最小限のコード。** スタイルシートには基本動作に必要なルールのみが含まれており、使用しないかもしれない位置・スタイル・アニメーションのクラスは含まれていません。
* **CSS による設定。** 各ツールチップは、CSS カスタムプロパティを通じてプロジェクトのニーズに応じた位置・外観・アニメーションを定義できます。
* **レイアウトシフトなし。** ポジショニングはブラウザのレイアウト計算中に行われ、レンダリング後に DOM を測定することはありません。
* **アクセシブル。** `aria-label` をコンテンツとして使用し、`:focus` 時にツールチップを表示します。
* **自動フォールバック。** CSS Anchor Positioning に対応していないブラウザは、上部中央の絶対配置を使用します。

> [!IMPORTANT]
> CSS Anchor Positioning は比較的新しいブラウザ機能です。対応していないブラウザは、動的配置ではなく予測可能なフォールバック（中央上部のバブル、絶対配置）を受け取ります。

## インストール

### npm

```bash
npm i @zkreations/tooltips
```

### フレームワークとバンドラー

パッケージはデフォルトのスタイルエントリとして圧縮された CSS をエクスポートします：

```js
import '@zkreations/tooltips';
```

アプリケーションのエントリポイントで一度だけインポートします：

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

同じインポートは Vite、Nuxt、SvelteKit、および CSS パッケージインポートをサポートする他のバンドラーでも動作します。バンドラーがパッケージのスタイルエントリを解決できない場合は、ファイルを直接インポートします：

```js
import '@zkreations/tooltips/index.min.css';
```

両方のパスをインポートしないでください——同じスタイルシートが含まれています。

### Sass

プロジェクトでソースをコンパイルする必要がある場合にのみ Sass エントリを使用します：

```scss
@use '@zkreations/tooltips/scss/tooltip';
```

その場合、パッケージの CSS もインポートしないでください。ほとんどのプロジェクトはコンパイル済みの CSS エントリを使用すべきです。

### CDN

```html
<link href="https://cdn.jsdelivr.net/npm/@zkreations/tooltips@5/index.min.css" rel="stylesheet"/>
```

## 使い方

任意の HTML 要素に `.tooltip` クラスと `aria-label` 属性を追加します：

```html
<button type="button" class="tooltip" aria-label="こんにちは！">
  ホバーするかフォーカスしてください
</button>
```

### ポジショニング

ツールチップはデフォルトで上部（`block-start`）に表示され、スペースが不足した場合は自動的に反転（`flip-block, flip-inline`）します：

```css
.tooltip::before {
  position-area: var(--tooltip-area, block-start);
  position-try-fallbacks: var(--tooltip-fallbacks, flip-block, flip-inline);
}
```

カスタム位置を設定するには、`--tooltip-area` を上書きします：

```css
.tooltip--right  { --tooltip-area: inline-end; }
.tooltip--left   { --tooltip-area: inline-start; }
.tooltip--bottom { --tooltip-area: block-end; }
```

自動切り替えなしで位置を固定するには：

```css
.tooltip--fixed-right {
  --tooltip-area: inline-end;
  --tooltip-fallbacks: none;
}
```

### プログラムによる表示

ホバーやフォーカスなしでツールチップを表示するには、`data-tooltip-visible` を追加します：

```html
<button type="button" class="tooltip" aria-label="アクティブな通知" data-tooltip-visible>
  通知
</button>
```

## カスタマイズ

CSS 変数を上書きして外観を調整します：

| 変数 | デフォルト値 | 説明 |
| --- | --- | --- |
| `--tooltip-area` | `block-start` | アンカーを基準とした位置エリア |
| `--tooltip-fallbacks` | `flip-block, flip-inline` | クリップされた場合のフォールバック位置 |
| `--tooltip-gap` | `0.5rem` | アンカーとツールチップの間隔 |
| `--tooltip-bg` | `rgb(0 0 0 / 90%)` | 背景色 |
| `--tooltip-color` | `#fff` | テキスト色 |
| `--tooltip-font-size` | `0.875rem` | フォントサイズ |
| `--tooltip-font-family` | `inherit` | フォントファミリー |
| `--tooltip-line-height` | `1.5` | 行の高さ |
| `--tooltip-padding` | `0.5em 0.75em` | バブルのパディング |
| `--tooltip-border` | `none` | バブルの境界線（ボーダー） |
| `--tooltip-border-radius` | `0.25em` | 境界線の丸み |
| `--tooltip-box-shadow` | `none` | バブルの影（ボックスシャドウ） |
| `--tooltip-max-width` | `20rem` | バブルの最大幅 |
| `--tooltip-duration` | `0.2s` | トランジションの時間 |
| `--tooltip-easing` | `ease` | トランジションのタイミング関数 |
| `--tooltip-scale` | `1` | バブルのスケール |
| `--tooltip-origin` | `center` | 変形の基点 |
| `--tooltip-x` | `0` | 水平オフセット |
| `--tooltip-y` | `0` | 垂直オフセット |
| `--tooltip-start-scale` | `--tooltip-scale` | 初期スケール |
| `--tooltip-end-scale` | `--tooltip-scale` | 表示時のスケール |
| `--tooltip-start-x` | `--tooltip-x` | 初期水平オフセット |
| `--tooltip-end-x` | `--tooltip-x` | 表示時の水平オフセット |
| `--tooltip-start-y` | `--tooltip-y` | 初期垂直オフセット |
| `--tooltip-end-y` | `--tooltip-y` | 表示時の垂直オフセット |

例：

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

## コンパクトバージョン

CSS 変数を使用せず、できるだけ軽量にしたい場合のために、本プロジェクトにはコンパクト版（`compact.css` / `compact.min.css`）が含まれています。CSS Anchor Positioning による自動配置と、非対応ブラウザ向けのフォールバックをそのまま維持しています。

非常に軽量（非圧縮で約 1 KB、圧縮後で約 800 B）であるため、外部依存関係として読み込むのではなく、[compact.css](compact.css) のコードをプロジェクトのスタイルシートに直接コピーして組み込むことを推奨します。これにより、変数に頼ることなく CSS で直接ツールチップのスタイル全体をカスタマイズできます。

パッケージからインポートして使用することも可能です：

```js
import '@zkreations/tooltips/compact.min.css';
```

## 矢印なし、それが設計上の選択

v5 は擬似要素の矢印（`::after`）を含んでいません。`flip-block` および `flip-inline` はバブルの配置を変えますが、その方向の変化をすべてのブラウザで一貫して擬似要素の境界線に伝えることができず、視覚的なバグを引き起こします。矢印を省略することでそれらのバグを回避し、スタイルシートをより小さく保ちます。

## ブラウザ互換性

- CSS Anchor Positioning をサポートするブラウザは `@supports (position-area: block-start)` を使用して動的配置と自動切り替えを行います。
- 未対応のブラウザは静的なフォールバックを受け取ります：上部中央の絶対配置バブル。
- 現在のサポート状況：[Can I Use — CSS Anchor Positioning](https://caniuse.com/css-anchor-positioning)。

## v4 から v5 への移行

| v4 | v5 |
| --- | --- |
| `[data-tts]` | `.tooltip` |
| `data-tts-visible` | `data-tooltip-visible` |
| `[data-tts="down"]` | `--tooltip-area: block-end;` |
| `[data-tts="left"]` | `--tooltip-area: inline-start;` |
| `[data-tts="right"]` | `--tooltip-area: inline-end;` |
| `--tts-*` | `--tooltip-*` |
| `tooltips.min.css` | `index.min.css` |

## サポート

このプロジェクトの維持を支援したい場合は、[コーヒーをごちそうしてください](https://ko-fi.com/zkreations)。

## ライセンス

MIT ライセンス
