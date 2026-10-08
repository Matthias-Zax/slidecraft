# SlideCraft Guidelines (copilot-instructions.md)

Welcome to **SlideCraft**, an agent-first Markdown toolkit for creating presentations and presenter cockpits.

<workflow>

## Core Architecture

All maintained content, instructions, and reusable code snippets live in Markdown. The slide-architect agent reads skills and generates HTML directly, without a compiler, `src/`, or package-based build pipeline.

Talk metadata lives in `talks/<talk-name>/talk.md` YAML frontmatter. Slides live in the talk's `slides/` directory. Generated HTML goes under `dist/<talk-name>/`:
- `audience.html` — Clean 16:9 projector display without clutter or speaker controls.
- `presenter.html` — Dual-screen presenter cockpit (preview, next slide, elapsed timer, live speaker notes).
- `deck.html` — Standalone presentation for reading or online sharing.

## Slide Markdown Conventions

Every slide lives in its own `.md` file inside `talks/<talk-name>/slides/<chapter>/`:
```markdown
---
title: "Slide Title"
subtitle: "One-sentence subtitle summarizing the key point"
layout: split-2col  # single, split-2col, 3col, math-focus, table-focus, closing
chapter: "Chapter Name"
footer: "Memorable fortune-cookie one-liner"
tags: ["tag1", "tag2"]
---

Slide body content in Markdown, with HTML component classes if needed.

<!-- note -->
[STAGE: Physical stage direction / movement]
Spoken words for the speaker. Aim for 60-90 seconds per slide.
Target time, pacing advice, and rhetorical questions.
<!-- endnote -->
```

## Agent Workflow

- Use `/create-slide` to author slide Markdown with the slide-components and speaker-coach skills.
- Use `/generate-talk <talk-name>` with slide-architect to generate all three HTML views directly using presentation-runtime and slide-components.
- Use `/rehearse-talk` to review pacing and delivery.
- Keep reusable HTML, CSS, and JavaScript in fenced blocks inside skill Markdown references.
- Treat generated HTML as disposable output. Update Markdown sources and regenerate instead of maintaining a separate runtime source tree.
- Verify generated structure and JavaScript syntax; browser testing is performed manually by the user, not through automated browser tests.

## Speaker Notes Standard

- Always include `[STAGE: ...]` cues for body language, vocal pacing, or slide timing.
- Write speaker notes as spoken narrative, not bullet points.
- Test that all slides can be delivered comfortably within the allotted talk time (typically 2-2.5 minutes per slide maximum).

</workflow>
