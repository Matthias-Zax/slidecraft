---
title: "The Zero-Sum Attention Budget"
subtitle: "Why Every Additional Token Dilutes Critical Rules"
layout: split-2col
chapter: "The Math"
footer: "Sum of attention weights is always identically 1.0 (100%)"
tags: ["math", "zero-sum", "budget"]
---

<div class="grid-2col" style="align-items: center;">
  <div>
    <div class="math-block" style="font-size: 24px;">
      $$a_{ij} = \frac{\exp(s_{ij})}{\sum_{m=1}^{N} \exp(s_{im})}$$
    </div>
    <div class="math-block" style="font-size: 22px; border-color: var(--neon-green);">
      $$\sum_{j=1}^{N} a_{ij} = 1.0 \quad (100\%)$$
    </div>
  </div>

  <div class="card-cyber highlight-cyan">
    <h3 style="color: #ffffff; margin-bottom: 12px;">The 100-Point Budget Rule</h3>
    <ul class="bullet-list" style="font-size: 18px;">
      <li><strong>Attention is a zero-sum game</strong>: Total weight is exactly 100 points.</li>
      <li><strong>50-token prompt</strong>: 3 critical rules share ~30 points each. Laser focus.</li>
      <li><strong>50,000-token prompt</strong>: Same rules receive ~0.05 points each. Crushed by noise.</li>
    </ul>
  </div>
</div>

<blockquote class="callout green" style="margin-top: 24px;">
  "You cannot increase the attention numerator without swelling the denominator. Every irrelevant line of code steals focus from your core requirement."
</blockquote>

<!-- note -->
[STAGE: Pause for emphasis. Use hand gestures to show shrinking budget]
Look at the denominator in this formula:
The sum from m=1 to N of exp(s_im).
N is the number of tokens in your context window.
When N is 50 tokens, the denominator is small. The model assigns 30% of its attention to your security requirement.
When N reaches 50,000 tokens—because of terminal logs, old stack traces, and 15 previous chat turns—the denominator explodes.
That same security rule that had 30% attention?
Its weight is crushed down to 0.05%.
Mathematically, the signal disappears into the exponential noise floor.
<!-- endnote -->
