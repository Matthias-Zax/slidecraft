# HTML Templates

Reusable source snippets. Read these blocks when generating HTML; do not recreate a source tree.

## audience.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>{{TALK_TITLE}} - Audience View</title>
  <style>
    /* {{THEME_CSS}} */
    /* {{COMPONENTS_CSS}} */
  </style>
</head>
<body>
  <div id="blackoutOverlay" class="blackout-overlay"></div>
  <div class="deck-container">
    <!-- {{SLIDES_HTML}} -->
  </div>

  <script>
    /* {{SYNC_ENGINE_JS}} */
  </script>
  <script>
    /* {{AUDIENCE_CONTROLLER_JS}} */
  </script>
</body>
</html>
```

## deck.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>{{TALK_TITLE}} - Interactive Deck</title>
  <style>
    /* {{THEME_CSS}} */
    /* {{COMPONENTS_CSS}} */
  </style>
</head>
<body>
  <div id="blackoutOverlay" class="blackout-overlay"></div>
  <div class="deck-container">
    <!-- {{SLIDES_HTML}} -->
  </div>

  <script>
    /* {{SYNC_ENGINE_JS}} */
  </script>
  <script>
    /* {{AUDIENCE_CONTROLLER_JS}} */
  </script>
</body>
</html>
```

## presenter.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>{{TALK_TITLE}} - Presenter Cockpit</title>
  <style>
    /* {{PRESENTER_CSS}} */
  </style>
</head>
<body class="presenter-mode">
  <div class="cockpit-layout">
    <!-- Header -->
    <header class="cockpit-header">
      <div class="cockpit-brand">
        <span>⚡ SLIDECRAFT COCKPIT</span>
        <span style="color: #64748b;">|</span>
        <span style="color: #cbd5e1;">{{TALK_TITLE}}</span>
      </div>
      <div class="cockpit-stats">
        <div class="slide-counter-badge" id="slideCounter">1 / --</div>
        <div class="timer-box" id="timerDisplay" title="Press 'T' to Pause/Resume, 'R' to Reset">00:00</div>
      </div>
    </header>

    <!-- Center Left: Split Previews -->
    <div class="previews-panel">
      <div class="preview-current">
        <div class="preview-label">Live on Projector</div>
        <iframe id="currentFrame" class="preview-frame" src="audience.html"></iframe>
      </div>
      <div class="preview-next">
        <div class="preview-label" style="color:#ffb700;">Up Next</div>
        <iframe id="nextFrame" class="preview-frame" src="audience.html"></iframe>
      </div>
    </div>

    <!-- Center Right: Speaker Notes -->
    <div class="notes-panel">
      <div class="notes-header">
        <span>Speaker Delivery Notes & Stage Cues</span>
        <span style="color: #00ff88;">Keys: Space/Arrows (Next), B (Blackout), T (Timer)</span>
      </div>
      <div class="notes-content" id="notesContent">
        Loading speaker notes...
      </div>
    </div>

    <!-- Bottom: Thumbnails / Chapter Strip -->
    <nav class="thumbnails-panel" id="thumbnailsContainer"></nav>
  </div>

  <script>
    window.SLIDECRAFT_DATA = /* {{SLIDES_DATA_JSON}} */;
  </script>
  <script>
    /* {{SYNC_ENGINE_JS}} */
  </script>
  <script>
    /* {{PRESENTER_CONTROLLER_JS}} */
  </script>
</body>
</html>
```
