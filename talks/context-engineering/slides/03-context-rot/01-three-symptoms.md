---
title: "The Three Pathologies of Context Rot"
subtitle: "How Attention Dilution Breaks Real Code in Real Projects"
layout: 3col
chapter: "Context Rot"
footer: "Diagnosing LLM performance collapse in prolonged sessions"
tags: ["symptoms", "context-rot", "bugs"]
---

<div class="grid-3col">
  <div class="card-cyber highlight-magenta">
    <div style="font-family: var(--font-mono); color: var(--neon-magenta); font-size: 20px; font-weight: 700;">1. Zombie Code</div>
    <div style="color: var(--text-muted); font-size: 13px; margin: 4px 0 12px 0;">NEGATIVE PRIMING</div>
    <p style="font-size: 16px; color: var(--text-dim); line-height: 1.45;">
      The model treats obsolete, broken code in early chat turns as the primary template for new generation.
    </p>
  </div>

  <div class="card-cyber highlight-amber">
    <div style="font-family: var(--font-mono); color: var(--neon-amber); font-size: 20px; font-weight: 700;">2. Constraint Bleed</div>
    <div style="color: var(--text-muted); font-size: 13px; margin: 4px 0 12px 0;">SOFTMAX DILUTION</div>
    <p style="font-size: 16px; color: var(--text-dim); line-height: 1.45;">
      Rules established in prompt #1 ("Never use Any", "Always write unit tests") fade out after 20 chat messages.
    </p>
  </div>

  <div class="card-cyber highlight-cyan">
    <div style="font-family: var(--font-mono); color: var(--neon-cyan); font-size: 20px; font-weight: 700;">3. Multi-Hop Collapse</div>
    <div style="color: var(--text-muted); font-size: 13px; margin: 4px 0 12px 0;">REASONING BREAKDOWN</div>
    <p style="font-size: 16px; color: var(--text-dim); line-height: 1.45;">
      Connecting 3+ architectural dependencies across 100k tokens becomes mathematically intractable.
    </p>
  </div>
</div>

<blockquote class="callout amber" style="margin-top: 24px;">
  "Context Rot is not a bug in the model weights—it is an inevitable consequence of prompt entropy over time."
</blockquote>

<!-- note -->
[STAGE: Connect with audience developer experience]
Every developer in this room has experienced Context Rot.
It usually starts around message 12 of a long chat session.
Symptom 1: Zombie Code. You told the model 5 minutes ago: "That library is deprecated, don't use it!" Yet it imports it again. Why? Because the broken code is sitting in the context window acting as a positive autoregressive prime.
Symptom 2: Constraint Bleed. You specified strict typing at the start. After 15 turns, it starts spitting out `any` and unhandled promises.
Symptom 3: Multi-Hop Collapse. It fixes line 42, but breaks the contract between the frontend DTO and the backend controller.
<!-- endnote -->
