---
title: "The Model Routing Matrix"
subtitle: "Matching Context Size and Reasoning Effort to the Real Task"
layout: table-focus
chapter: "Solutions"
footer: "Stick to the diagonal: Never combine maximum context with maximum reasoning"
tags: ["routing", "matrix", "architecture"]
---

<table class="table-cyber">
  <thead>
    <tr>
      <th>Context Size</th>
      <th>Reasoning Effort</th>
      <th>Ideal Workload</th>
      <th>Production Verdict</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong style="color:var(--neon-green);">Minimal (&lt;16k)</strong></td>
      <td><strong>High (Reasoning)</strong></td>
      <td>Complex refactoring, concurrency bugs, TDD loops, security review</td>
      <td><span style="color:var(--neon-green);">★ SWEET SPOT: Zero rot, surgical precision</span></td>
    </tr>
    <tr>
      <td><strong style="color:var(--neon-cyan);">Massive (1M+)</strong></td>
      <td><strong>Low (Scan)</strong></td>
      <td>Repository audits, API drift detection, legacy codebase mapping</td>
      <td><span style="color:var(--neon-cyan);">★ SWEET SPOT: Broad synthesis, fast scan</span></td>
    </tr>
    <tr>
      <td><strong style="color:var(--neon-magenta);">Massive (1M+)</strong></td>
      <td><strong style="color:var(--neon-magenta);">High (Reasoning)</strong></td>
      <td>"Debug this entire monorepo with 50 previous chat turns"</td>
      <td><span style="color:var(--neon-magenta);">✖ DANGER ZONE: 10x latency, context rot, collapse</span></td>
    </tr>
  </tbody>
</table>

<blockquote class="callout amber" style="margin-top: 24px;">
  "Golden Engineering Law: If you need deep reasoning, make context small. If you need wide context, keep reasoning shallow."
</blockquote>

<!-- note -->
[STAGE: Walk across stage, deliver with authority]
Remember this table. Write it down.
There are two legitimate sweet spots in modern AI engineering:
Sweet spot one: Minimal context (<16k tokens) with maximum reasoning. This is for surgical coding, complex bug fixing, and test-driven development. No context rot, zero hallucinations.
Sweet spot two: Massive context (1M+ tokens) with low reasoning. This is for scanning entire repos, finding deprecated API calls, and generating high-level summaries.
The fatal mistake developers make is row 3:
Dumping 500k tokens and demanding deep multi-hop reasoning.
You get 60-second latencies, massive dollar costs, and complete reasoning collapse.
Stay on the diagonal!
<!-- endnote -->
