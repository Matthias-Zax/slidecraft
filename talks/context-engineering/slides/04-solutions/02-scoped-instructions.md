---
title: "Scoped Context via applyTo Globs"
subtitle: "Loading Rules on Demand to Preserve Attention Mass"
layout: split-2col
chapter: "Solutions"
footer: "VS Code Scoped Instructions Pattern: .github/instructions/*.instructions.md"
tags: ["globs", "vscode", "scoped"]
---

<div class="grid-2col">
  <div>
    <h3 style="color: var(--neon-cyan); margin-bottom: 12px;">The Fat Prompt Anti-Pattern</h3>
    <pre class="code-block"><code class="language-markdown"># Mega Prompt (Loaded Everywhere)
- React conventions... (40 lines)
- PostgreSQL rules... (50 lines)
- Spring Boot architecture... (60 lines)
- Kubernetes YAML syntax... (30 lines)

Total: 180 lines in EVERY prompt!
Attention wasted: ~80%</code></pre>
  </div>

  <div>
    <h3 style="color: var(--neon-green); margin-bottom: 12px;">The Scoped Pattern</h3>
    <pre class="code-block"><code class="language-yaml">---
applyTo: "frontend/src/**/*.ts"
---
# Angular Rules
- Always use OnPush change detection
- Use signals for reactive local state
- Freya design system components only

Total: 15 lines (loaded only when needed!)</code></pre>
  </div>
</div>

<blockquote class="callout" style="margin-top: 24px;">
  "By scoping rules to file globs, the LLM receives maximum attention density on the relevant technology stack."
</blockquote>

<!-- note -->
[STAGE: Point out the contrast between left and right code blocks]
Here is the concrete difference in code.
On the left: The Mega Prompt. Developers dump their entire tech stack into one giant prompt file.
When you are tweaking a CSS button, the model is still loading 50 lines of PostgreSQL foreign key rules.
That is wasted attention denominator mass.
On the right: Scoped instructions with `applyTo` globs.
The Angular rules are only loaded when you edit TypeScript files in `frontend/src/`.
When you switch to backend Java files, those tokens vanish and make room for Spring Boot rules.
Clean counter. Zero denominator bloat.
<!-- endnote -->
