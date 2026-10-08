---
name: presentation-runtime
description: 'Generate self-contained SlideCraft HTML presentations from Markdown talks. Use when generating a deck, audience display, or presenter cockpit with navigation, speaker notes, timers, and synchronized screens.'
---

# Presentation Runtime

<workflow>

## Source References

- [HTML templates](./references/templates.md): audience, deck, and presenter shells.
- [JavaScript controllers](./references/controllers.md): navigation, timers, and synchronization.
- [Presentation styles](../slide-components/references/styles.md): theme, components, and cockpit CSS.

These fenced blocks are reusable starting points, not an executable build system. Adapt them directly into generated HTML. Do not create a compiler, package manifest, or `src/` directory.

## Generation Workflow

1. Read `talks/<talk-name>/talk.md` for title, subtitle, speaker, theme, aspect ratio, and target minutes. Read slides in sorted chapter and filename order.
2. Interpret slide YAML frontmatter as metadata, not visible content. Separate `<!-- note -->` through `<!-- endnote -->` from the body. Render Markdown headings, lists, tables, emphasis, and code fences into HTML; preserve intentional HTML components.
3. Render each slide as a `.slide` section inside `.deck-container`, with header, body, and footer. Mark only the first slide `active`. Preserve titles, chapters, subtitles, footer quotes, speaker attribution, and slide numbering.
4. Use the audience and deck templates with theme and component styles. Use the presenter template with cockpit styles and an ordered `window.SLIDECRAFT_DATA` array containing `{ index, id, meta, notes }` for each slide.
5. Inline CSS and JavaScript and replace every `{{...}}` placeholder. Escape text for its HTML context. Serialize data with JSON and escape `<` as `\u003c` in inline scripts so slide text cannot terminate a script element.
6. Write `audience.html`, `presenter.html`, and `deck.html` under `dist/<talk-name>/`. Presenter preview URLs must point to its sibling audience file. Keep notes out of both audience and deck output.

## Required Runtime Adaptations

The reference code preserves the original implementation. Apply these requirements during generation rather than copying it blindly:

- Use a talk-specific channel, such as `slidecraft:<talk-name>`, consistently in presenter and audience. The standalone deck must navigate independently and not publish into the live presentation channel.
- Isolate the current and next preview iframes from live synchronization. For example, add `?preview=1` to their URLs, skip channel initialization in preview mode, and accept `GOTO_SLIDE` messages only from `window.parent`.
- Send preview indices after each iframe loads as well as when navigating. At the final slide, show an explicit end-of-talk preview rather than retaining an earlier slide.
- On audience connection or reload, request current slide and blackout state from the presenter. Reply with current state rather than resetting an ongoing presentation.
- Derive timer warning and overtime thresholds from `targetMinutes`, not the hard-coded 20/25-minute defaults.
- Treat speaker notes as text. Build stage-cue highlights safely rather than injecting unescaped notes into `innerHTML`.
- Add viewport metadata, constrain cockpit panels, and adapt the presenter layout for narrow screens without overlapping notes or controls.
- Render math with KaTeX when needed. For fully offline output, inline its required runtime, styles, and font resources; do not silently rely on a CDN. If those resources are unavailable, disclose the limitation instead of claiming offline math support.

## Example

Request: `/generate-talk context-engineering`

Output: `dist/context-engineering/audience.html`, `presenter.html`, and `deck.html`, generated from the talk's Markdown metadata and twelve ordered slides without a build pipeline.

## Verification

Check slide counts, ordering, notes separation, relative preview paths, resolved placeholders, and JavaScript syntax without automated browser tests. Ask the user to manually verify both screens, current and next previews, late audience connection, navigation boundaries, blackout, timer controls, and desktop/mobile layout.

Opening the HTML files directly is sufficient for deck reading. Cross-window synchronization on `file:` URLs varies by browser; if needed, serve the generated directory from the same local HTTP origin using an available static server, without introducing a maintained build pipeline.

</workflow>
