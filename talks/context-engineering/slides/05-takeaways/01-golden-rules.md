---
title: "The 5 Golden Rules of Context Engineering"
subtitle: "What You Should Do Tomorrow Morning at Your Desk"
layout: split-2col
chapter: "Takeaways"
footer: "Practical heuristics for daily AI-assisted software engineering"
tags: ["rules", "takeaways", "heuristics"]
---

<div class="grid-2col">
  <div class="card-cyber">
    <ul class="bullet-list" style="font-size: 18px;">
      <li><strong>1. The 15-Message Rule:</strong> When a task is complete or goes off track, start a fresh chat (`Ctrl+L`). Don't argue with zombie code.</li>
      <li><strong>2. Document the Unique:</strong> Only put things in instructions that the model cannot know from pretraining.</li>
      <li><strong>3. Scope Everything:</strong> Use `applyTo` globs instead of giant monolithic instruction files.</li>
    </ul>
  </div>

  <div class="card-cyber highlight-green">
    <ul class="bullet-list" style="font-size: 18px;">
      <li><strong>4. Mind the U-Curve:</strong> Put mission-critical constraints at the very top or in the final prompt, never in the middle.</li>
      <li><strong>5. Stay on the Diagonal:</strong> High reasoning demands tiny context. Broad context demands shallow tasks.</li>
    </ul>
  </div>
</div>

<blockquote class="callout green" style="margin-top: 24px;">
  "Context is a scarce attention budget, not a garbage bin. Engineer it with the same discipline you engineer your database queries."
</blockquote>

<!-- note -->
[STAGE: Stand center stage, project confidence]
Here are five concrete rules you can take back to your teams on Monday morning:
Rule 1: The 15-Message Rule. Don't spend 20 minutes arguing with a confused model. Clear the prep counter. Start fresh.
Rule 2: Document the unique, not the universal.
Rule 3: Scope instructions with globs.
Rule 4: Respect the U-curve. Critical rules go at the bookends, never buried in middle noise.
Rule 5: Stay on the diagonal. High reasoning requires minimal context.
<!-- endnote -->
