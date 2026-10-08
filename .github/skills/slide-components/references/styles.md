# Presentation Styles

Reusable source snippets. Read these blocks when generating HTML; do not recreate a source tree.

## components.css

```css
/* slidecraft/src/css/components.css */

/* Layout Grids */
.grid-2col {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 32px;
  align-items: stretch;
}

.grid-3col {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
  align-items: stretch;
}

/* Card primitives */
.card-cyber {
  background: var(--bg-card);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 8px;
  padding: 24px;
  position: relative;
  overflow: hidden;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.25);
}

.card-cyber.highlight-cyan {
  border-color: rgba(0, 240, 255, 0.4);
  box-shadow: 0 0 20px rgba(0, 240, 255, 0.08);
}

.card-cyber.highlight-green {
  border-color: rgba(0, 255, 136, 0.4);
  box-shadow: 0 0 20px rgba(0, 255, 136, 0.08);
}

.card-cyber.highlight-amber {
  border-color: rgba(255, 183, 0, 0.4);
  box-shadow: 0 0 20px rgba(255, 183, 0, 0.08);
}

/* Metric Display Cards */
.metric-box {
  background: var(--bg-card);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 8px;
  padding: 24px 20px;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.metric-value {
  font-family: var(--font-mono);
  font-size: 56px;
  font-weight: 800;
  line-height: 1.1;
  color: var(--neon-cyan);
  text-shadow: 0 0 24px rgba(0, 240, 255, 0.3);
}

.metric-value.amber {
  color: var(--neon-amber);
  text-shadow: 0 0 24px rgba(255, 183, 0, 0.3);
}

.metric-value.green {
  color: var(--neon-green);
  text-shadow: 0 0 24px rgba(0, 255, 136, 0.3);
}

.metric-label {
  font-size: 15px;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--text-muted);
  margin-top: 6px;
  font-weight: 600;
}

.metric-desc {
  font-size: 15px;
  color: var(--text-dim);
  margin-top: 10px;
  line-height: 1.4;
}

/* Bullet list */
.bullet-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.bullet-list li {
  position: relative;
  padding-left: 28px;
  font-size: 20px;
  line-height: 1.45;
  color: var(--text-main);
}

.bullet-list li strong {
  color: #ffffff;
}

.bullet-list li::before {
  content: '▶';
  position: absolute;
  left: 0;
  top: 1px;
  font-size: 12px;
  color: var(--neon-cyan);
}

/* Callout blocks */
.callout {
  border-left: 4px solid var(--neon-cyan);
  background: rgba(0, 240, 255, 0.06);
  padding: 18px 24px;
  border-radius: 0 8px 8px 0;
  font-size: 20px;
  color: #ffffff;
  margin: 16px 0;
}

.callout.amber {
  border-left-color: var(--neon-amber);
  background: rgba(255, 183, 0, 0.06);
}

.callout.green {
  border-left-color: var(--neon-green);
  background: rgba(0, 255, 136, 0.06);
}

/* Code & Syntax */
code {
  font-family: var(--font-mono);
  background: rgba(255, 255, 255, 0.08);
  padding: 2px 8px;
  border-radius: 4px;
  color: var(--neon-cyan);
  font-size: 0.9em;
}

pre.code-block {
  background: #06080b;
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 8px;
  padding: 18px 22px;
  overflow-x: auto;
  font-family: var(--font-mono);
  font-size: 16px;
  line-height: 1.5;
  color: #cbd5e1;
}

/* Math equations */
.math-block {
  background: #080a0f;
  border: 1px solid rgba(0, 240, 255, 0.2);
  border-radius: 8px;
  padding: 18px 24px;
  margin: 16px 0;
  text-align: center;
  font-size: 24px;
  color: #ffffff;
  box-shadow: inset 0 0 15px rgba(0, 0, 0, 0.5);
}

.math-inline {
  font-family: serif;
  font-style: italic;
  color: var(--neon-green);
  padding: 0 4px;
}

/* Comparison Tables */
.table-cyber {
  width: 100%;
  border-collapse: collapse;
  font-size: 17px;
  margin: 12px 0;
}

.table-cyber th {
  text-align: left;
  padding: 12px 16px;
  background: rgba(255, 255, 255, 0.04);
  color: var(--neon-cyan);
  border-bottom: 2px solid rgba(255, 255, 255, 0.1);
  font-family: var(--font-mono);
  text-transform: uppercase;
  font-size: 13px;
  letter-spacing: 0.08em;
}

.table-cyber td {
  padding: 14px 16px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
  color: var(--text-main);
}

.table-cyber tr:hover td {
  background: rgba(255, 255, 255, 0.02);
}
```

## presenter.css

```css
/* slidecraft/src/css/presenter.css */
body.presenter-mode {
  background: #06070a;
  color: #e2e8f0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  overflow: hidden;
  height: 100vh;
  margin: 0;
  padding: 0;
}

.cockpit-layout {
  display: grid;
  grid-template-rows: 60px 1fr 140px;
  grid-template-columns: 1.15fr 0.85fr;
  height: 100vh;
  gap: 12px;
  padding: 12px;
  box-sizing: border-box;
}

/* Header Bar */
.cockpit-header {
  grid-column: 1 / -1;
  background: #0f131a;
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 6px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 24px;
}

.cockpit-brand {
  font-family: 'JetBrains Mono', monospace;
  font-size: 16px;
  font-weight: 700;
  color: #00f0ff;
  letter-spacing: 0.05em;
  display: flex;
  align-items: center;
  gap: 12px;
}

.cockpit-stats {
  display: flex;
  align-items: center;
  gap: 32px;
}

.timer-box {
  display: flex;
  align-items: center;
  gap: 8px;
  font-family: 'JetBrains Mono', monospace;
  font-size: 26px;
  font-weight: 700;
  color: #00ff88;
}

.timer-box.warning {
  color: #ffb700;
}

.timer-box.overtime {
  color: #f43f5e;
}

.slide-counter-badge {
  font-family: 'JetBrains Mono', monospace;
  font-size: 16px;
  color: #94a3b8;
  background: rgba(255, 255, 255, 0.05);
  padding: 4px 12px;
  border-radius: 4px;
}

/* Center Left: Previews */
.previews-panel {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.preview-current {
  flex: 2;
  background: #0a0c10;
  border: 2px solid #00f0ff;
  border-radius: 6px;
  position: relative;
  overflow: hidden;
  display: flex;
  flex-direction: column;
}

.preview-next {
  flex: 1.2;
  background: #0a0c10;
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 6px;
  position: relative;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  opacity: 0.85;
}

.preview-label {
  position: absolute;
  top: 8px;
  left: 8px;
  z-index: 10;
  background: rgba(0, 0, 0, 0.75);
  padding: 3px 8px;
  font-size: 11px;
  font-family: 'JetBrains Mono', monospace;
  border-radius: 3px;
  color: #00f0ff;
  text-transform: uppercase;
}

.preview-frame {
  width: 100%;
  height: 100%;
  border: none;
  pointer-events: none;
}

/* Center Right: Speaker Notes & Cues */
.notes-panel {
  background: #0f131a;
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 6px;
  display: flex;
  flex-direction: column;
  padding: 24px;
  overflow-y: auto;
}

.notes-header {
  font-family: 'JetBrains Mono', monospace;
  font-size: 13px;
  text-transform: uppercase;
  color: #94a3b8;
  letter-spacing: 0.1em;
  margin-bottom: 16px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
  padding-bottom: 8px;
  display: flex;
  justify-content: space-between;
}

.notes-content {
  font-size: 21px;
  line-height: 1.6;
  color: #f1f5f9;
  white-space: pre-wrap;
  word-break: break-word;
}

.notes-content strong {
  color: #00ff88;
}

.notes-content .stage-cue {
  display: block;
  background: rgba(255, 183, 0, 0.12);
  border-left: 3px solid #ffb700;
  padding: 8px 12px;
  margin: 12px 0;
  font-size: 17px;
  color: #ffd269;
}

/* Bottom: Thumbnails / Chapter strip */
.thumbnails-panel {
  grid-column: 1 / -1;
  background: #0f131a;
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 6px;
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 16px;
  overflow-x: auto;
}

.thumb-card {
  flex: 0 0 160px;
  height: 90px;
  background: #141923;
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 4px;
  cursor: pointer;
  padding: 8px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  transition: all 0.2s ease;
}

.thumb-card:hover {
  border-color: rgba(0, 240, 255, 0.5);
  background: #1b212f;
}

.thumb-card.active {
  border: 2px solid #00f0ff;
  background: #1e2638;
}

.thumb-title {
  font-size: 12px;
  font-weight: 600;
  color: #e2e8f0;
  line-height: 1.25;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.thumb-meta {
  font-family: 'JetBrains Mono', monospace;
  font-size: 10px;
  color: #94a3b8;
  display: flex;
  justify-content: space-between;
}
```

## theme-cyberpunk.css

```css
/* slidecraft/src/css/theme-cyberpunk.css */
:root {
  --bg-primary: #0a0c10;
  --bg-card: #12161f;
  --bg-card-hover: #181d29;
  --bg-surface: #1e2433;
  --text-main: #e2e8f0;
  --text-dim: #94a3b8;
  --text-muted: #64748b;
  
  /* Cyberpunk Neons */
  --neon-cyan: #00f0ff;
  --neon-green: #00ff88;
  --neon-amber: #ffb700;
  --neon-magenta: #f43f5e;
  --neon-purple: #a855f7;

  /* Font stacks */
  --font-display: 'Inter', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  --font-body: 'Inter', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  --font-mono: 'JetBrains Mono', 'Fira Code', 'Consolas', monospace;

  --slide-width: 1280px;
  --slide-height: 720px;
  --slide-aspect: calc(16 / 9);
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background-color: #050608;
  color: var(--text-main);
  font-family: var(--font-body);
  font-size: 20px;
  line-height: 1.5;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

/* Master Slide Canvas */
.deck-container {
  width: var(--slide-width);
  height: var(--slide-height);
  position: relative;
  overflow: hidden;
  background-color: var(--bg-primary);
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.7);
  border-radius: 8px;
}

.slide {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  padding: 56px 64px 48px 64px;
  display: flex;
  flex-direction: column;
  opacity: 0;
  visibility: hidden;
  pointer-events: none;
  transition: opacity 0.3s cubic-bezier(0.16, 1, 0.3, 1), transform 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  transform: scale(0.985);
  background: radial-gradient(circle at top right, rgba(0, 240, 255, 0.05) 0%, transparent 50%),
              radial-gradient(circle at bottom left, rgba(0, 255, 136, 0.03) 0%, transparent 40%),
              var(--bg-primary);
}

.slide.active {
  opacity: 1;
  visibility: visible;
  pointer-events: auto;
  transform: scale(1);
}

/* Header */
.slide-header {
  margin-bottom: 28px;
}

.slide-tag {
  display: inline-block;
  font-family: var(--font-mono);
  font-size: 13px;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  padding: 3px 10px;
  border-radius: 4px;
  background: rgba(0, 240, 255, 0.12);
  color: var(--neon-cyan);
  border: 1px solid rgba(0, 240, 255, 0.3);
  margin-bottom: 12px;
}

.slide-title {
  font-size: 40px;
  font-weight: 800;
  letter-spacing: -0.02em;
  color: #ffffff;
  line-height: 1.15;
}

.slide-subtitle {
  font-size: 20px;
  color: var(--text-dim);
  margin-top: 6px;
  font-weight: 400;
}

/* Body & Content */
.slide-body {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
  z-index: 2;
}

/* Footer */
.slide-footer {
  margin-top: auto;
  padding-top: 16px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-top: 1px solid rgba(255, 255, 255, 0.08);
  font-family: var(--font-mono);
  font-size: 13px;
  color: var(--text-muted);
}

.footer-quote {
  color: var(--neon-green);
  font-style: italic;
}

/* Blackout overlay for projector */
.blackout-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: #000000;
  z-index: 9999;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.25s ease;
}

.blackout-overlay.active {
  opacity: 1;
  pointer-events: auto;
}
```
