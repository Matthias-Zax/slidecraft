---
title: "Attention Budgeting in Practice"
subtitle: "Architecting Context Like You Architect Memory Hierarchy"
layout: 3col
chapter: "Solutions"
footer: "Context Engineering Tier: Global -> Scoped -> Dynamic Inline"
tags: ["solutions", "budgeting", "instructions"]
---

<div class="grid-3col">
  <div class="card-cyber">
    <div style="font-family: var(--font-mono); color: var(--neon-cyan); font-size: 18px; font-weight: 700;">Level 1: Global</div>
    <div style="color: var(--text-muted); font-size: 12px; margin-bottom: 12px;">REPO LEVEL (L0)</div>
    <p style="font-size: 15px; color: var(--text-dim); line-height: 1.45;">
      Universal facts only: Java 21, Spring Boot 3.4, no Lombok, tabs vs spaces.
    </p>
    <div style="margin-top: 12px; font-size: 13px; color: var(--neon-green); font-family: var(--font-mono);">
      Target: &lt; 50 lines
    </div>
  </div>

  <div class="card-cyber highlight-green">
    <div style="font-family: var(--font-mono); color: var(--neon-green); font-size: 18px; font-weight: 700;">Level 2: Scoped</div>
    <div style="color: var(--text-muted); font-size: 12px; margin-bottom: 12px;">DIRECTORY LEVEL (L1)</div>
    <p style="font-size: 15px; color: var(--text-dim); line-height: 1.45;">
      Triggered only on matching files via <code>applyTo: "frontend/**"</code> or <code>applyTo: "*.sql"</code>.
    </p>
    <div style="margin-top: 12px; font-size: 13px; color: var(--neon-green); font-family: var(--font-mono);">
      Zero token cost until invoked
    </div>
  </div>

  <div class="card-cyber">
    <div style="font-family: var(--font-mono); color: var(--neon-amber); font-size: 18px; font-weight: 700;">Level 3: Inline</div>
    <div style="color: var(--text-muted); font-size: 12px; margin-bottom: 12px;">TASK LEVEL (L2)</div>
    <p style="font-size: 15px; color: var(--text-dim); line-height: 1.45;">
      Precise task context: <code>#file:orderService.ts</code> + acceptance criteria for the current turn.
    </p>
    <div style="margin-top: 12px; font-size: 13px; color: var(--neon-green); font-family: var(--font-mono);">
      Discarded on task completion
    </div>
  </div>
</div>

<blockquote class="callout green" style="margin-top: 24px;">
  "Document the unique, not the universal. If an LLM already knows it from its pretraining, do NOT put it in your system instructions."
</blockquote>

<!-- note -->
[STAGE: Walk audience through practical implementation]
So how do we engineer context correctly?
We use Attention Budgeting.
We treat context like a memory cache hierarchy:
Level 1: Global instructions. Keep this under 50 lines. Only write down what makes your project unique. Never teach the model what a REST API is—it already knows.
Level 2: Scoped instructions. Use `applyTo` globs. If you are editing an Angular component, don't load the SQL database conventions. Keep the denominator lean.
Level 3: Task-level inline context. Point to the specific file `#file` and the specific function. When the task is done, clear the session.
<!-- endnote -->
