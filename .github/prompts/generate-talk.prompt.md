---
name: generate-talk
description: 'Generate audience, presenter, and standalone HTML files directly from a Markdown talk using SlideCraft skills.'
agent: slide-architect
---

Generate HTML for the requested talk using the presentation-runtime and slide-components skills.

1. Use the talk named in my request. If none is named and only one talk exists, use it; otherwise ask which talk to generate.
2. Read its `talk.md` and all slide Markdown files in chapter and filename order.
3. Generate `dist/<talk-name>/audience.html`, `presenter.html`, and `deck.html` directly using the fenced snippets in the skills' Markdown references.
4. Preserve speaker notes and stage cues only in the presenter output. Apply the runtime skill's synchronization, preview, timer, escaping, and offline-resource requirements.
5. Do not introduce a compiler, `src/`, package dependencies, or a build pipeline.
6. Check the generated files structurally, then provide clickable output paths and a short manual verification checklist. Do not run automated browser tests.