# SlideCraft

An agent-first Markdown toolkit for technical presentations. Maintain slides, talk metadata, agents, prompts, and reusable code snippets as Markdown. Ask the agent to generate HTML directly when you need a deck.

There is no compiler, maintained runtime source tree, package manifest, or npm build step.

## Workflow

1. Select the `slide-architect` agent in VS Code.
2. Use `/create-slide` to create or update slides with layout components, speaker notes, and stage cues.
3. Use `/generate-talk context-engineering` to generate the audience, presenter, and standalone HTML views from the talk's Markdown sources.
4. Use `/rehearse-talk` to review narrative flow and pacing against the talk's target duration.

Generation uses the [presentation-runtime skill](.github/skills/presentation-runtime/SKILL.md) and the [slide-components skill](.github/skills/slide-components/SKILL.md). Their Markdown references contain fenced HTML, CSS, and JavaScript snippets. Outputs may vary between generations; this is an agent-guided workflow, not a deterministic build.

## Structure

```text
.github/
   copilot-instructions.md
   agents/
      slide-architect.agent.md
   prompts/
      create-slide.prompt.md
      generate-talk.prompt.md
      rehearse-talk.prompt.md
   skills/
      slide-components/
         SKILL.md
         references/
            styles.md
            two-column-split.md
      presentation-runtime/
         SKILL.md
         references/
            templates.md
            controllers.md
      speaker-coach/SKILL.md
      context-engineering/SKILL.md
talks/
   context-engineering/
      talk.md
      slides/<chapter>/<slide>.md
dist/<talk-name>/
   audience.html
   presenter.html
   deck.html
```

Everything maintained is Markdown. HTML under `dist/` is generated output. Existing outputs were retained during the conversion; regenerate them to apply the new workflow.

## Talk Sources

Use [the example talk metadata](talks/context-engineering/talk.md) as a starting point for a new talk. Its YAML frontmatter records `title`, `subtitle`, `speaker`, `theme`, `aspectRatio`, and `targetMinutes`.

Keep one slide per Markdown file under `talks/<talk-name>/slides/<chapter>/`. Chapter directories and slide filenames determine order. Each slide has YAML metadata, a Markdown/HTML body, and spoken notes between `<!-- note -->` and `<!-- endnote -->`. Include `[STAGE: ...]` cues. See [the authoring conventions](.github/copilot-instructions.md).

To change reusable styling or behavior, edit the skill's fenced snippets and regenerate. Do not recreate `src/`, `build/`, or package-based infrastructure.

## Presenting

Open the generated `presenter.html` on your laptop and its sibling `audience.html` on the projector in extended-display mode. Open `deck.html` for independent reading or sharing. Keep all three files together for presenter previews.

Navigation uses arrows, Space, or Page Up/Down. `B` toggles blackout; `T` pauses/resumes the presenter timer; `R` resets it.

Verify manually that both screens synchronize, previews show current and next slides, notes are private, timers work, and layouts fit desktop and mobile screens. Automated browser testing is not part of this workflow.

Direct file opening works for deck reading. If your browser does not synchronize local files, serve the generated directory from one local HTTP origin with an available static server. Offline math requires embedded KaTeX resources; the agent must report any unavailable resources rather than silently add CDN dependencies.

## Toolkit Validation

For the external Agent Markdown Linter Suite, lint customization entry points with `.github/agents/*.agent.md`, `.github/prompts/*.prompt.md`, `.github/skills/*/SKILL.md`, and `.github/copilot-instructions.md`.

Do not pass `.github/**/*.md` to that suite: it currently classifies Markdown reference documents as skill entry points and incorrectly requires their own frontmatter and short code blocks. Check reference links and the syntax of fenced JavaScript separately.

