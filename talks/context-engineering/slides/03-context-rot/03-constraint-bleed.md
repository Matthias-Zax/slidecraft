---
title: "Rotary Position Embeddings (RoPE)"
subtitle: "The 'Lost in the Middle' Phenomenon Is Built Into Math"
layout: split-2col
chapter: "The Math"
footer: "Liu et al. (2023) - Lost in the Middle: How Language Models Use Long Contexts"
tags: ["rope", "lost-in-middle", "embeddings"]
---

<div class="grid-2col" style="align-items: center;">
  <div>
    <h3 style="color: var(--neon-cyan); margin-bottom: 16px;">The Attention Distribution Curve</h3>
    <ul class="bullet-list" style="font-size: 18px;">
      <li><strong>Primacy Effect (Start):</strong> System prompts and instructions receive high initial attention.</li>
      <li><strong>Recency Effect (End):</strong> The latest user prompt receives high immediate attention.</li>
      <li><strong>The Middle Valley (Trough):</strong> Tokens placed between 20% and 80% of context suffer severe attention decay.</li>
    </ul>
  </div>

  <div class="card-cyber highlight-cyan" style="text-align: center; padding: 32px 20px;">
    <div style="font-family: var(--font-mono); color: var(--neon-amber); font-size: 48px; font-weight: 800;">U-Curve</div>
    <div class="metric-label">Attention Distribution Profile</div>
    <div style="margin-top: 16px; font-size: 15px; color: var(--text-dim); text-align: left; line-height: 1.6;">
      <span style="color:var(--neon-green)">▲ START:</span> System Prompt (High Attention)<br>
      <span style="color:var(--neon-magenta)">▼ MIDDLE:</span> <strong>The Dead Zone (Attenuated)</strong><br>
      <span style="color:var(--neon-cyan)">▲ END:</span> Current Query (High Attention)
    </div>
  </div>
</div>

<blockquote class="callout" style="margin-top: 24px;">
  "Never put critical architectural constraints in the middle of a 100k-token prompt. If it must be followed, place it at the root or right before generation."
</blockquote>

<!-- note -->
[STAGE: Draw a U-curve in the air with hand]
In 2023, Stanford and UC Berkeley published a landmark paper: "Lost in the Middle".
They proved that modern LLMs using Rotary Position Embeddings (RoPE) don't attend to context uniformly.
The attention curve forms a sharp 'U'.
The start of the context—your system instructions—gets high weight.
The end of the context—your latest question—gets high weight.
Everything in between? It falls into the attention dead zone.
If you dump a 400-page API documentation PDF into the prompt, the model will faithfully read the preface and the index, and completely forget chapter 14 in the middle.
<!-- endnote -->
