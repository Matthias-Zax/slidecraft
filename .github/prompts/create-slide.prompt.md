---
name: create-slide
description: Scaffold a new conference slide in SlideCraft with frontmatter, Cyberpunk layout, and stage-ready speaker cues.
agent: slide-architect
---

Help me create a new slide for the current talk.

Read the talk's `talk.md` and load the slide-components and speaker-coach skills. Write the slide directly under `talks/<talk-name>/slides/<chapter>/`; do not generate HTML unless requested.

Please provide:
1. **Title & Subtitle**: High-impact phrasing, scannable from distance.
2. **Layout**: One of `split-2col`, `3col`, `metric-focus`, `math-focus`, `table-focus`, `closing`.
3. **Slide Body**: Concise bullets or components. Bold the keyword, dim the rest.
4. **Speaker Notes (`<!-- note -->`)**:
   - `[STAGE: ...]` physical cues
   - Conversational, spoken words (no robotic bullets)
   - Anticipated delivery time (e.g. 90 seconds)
