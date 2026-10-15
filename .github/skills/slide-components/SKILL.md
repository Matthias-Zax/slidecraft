---
name: slide-components
description: 'Reusable HTML and CSS snippets for SlideCraft Cyberpunk presentations. Use when authoring slide layouts, choosing components, or generating styled HTML decks.'
---

# SlideCraft Slide Components

<workflow>

Use these standard HTML component classes when authoring slides in SlideCraft:

Read [presentation styles](./references/styles.md) for the complete theme, component, and presenter CSS snippets. Inline the required styles into generated HTML; Markdown references are the maintained source, not separate CSS files.

## 1. Two-Column Split Layout

Use the [two-column split layout example](./references/two-column-split.md).

## 2. Metric Highlight Box

```html
<div class="metric-box">
  <div class="metric-value">2M</div>
  <div class="metric-label">Token Context Window</div>
  <div class="metric-desc">Description of impact</div>
</div>
```

## 3. Cyber Callout Block

```html
<blockquote class="callout green">
  "Memorable conference quote or golden law goes here."
</blockquote>
```

## 4. Mathematical Equation Block

```html
<div class="math-block">
  $$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$
</div>
```

</workflow>
