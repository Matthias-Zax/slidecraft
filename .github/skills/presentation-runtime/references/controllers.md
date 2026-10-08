# Presentation Controllers

Reusable source snippets. Read these blocks when generating HTML; do not recreate a source tree.

## audience-controller.js

```javascript
// slidecraft/src/js/audience-controller.js
(function() {
  const sync = new window.SlideSyncEngine('slidecraft_presentation_channel');
  const slides = document.querySelectorAll('.slide');
  const blackout = document.getElementById('blackoutOverlay');
  let currentIndex = 0;

  function showSlide(index) {
    if (index < 0 || index >= slides.length) return;
    slides[currentIndex]?.classList.remove('active');
    currentIndex = index;
    slides[currentIndex]?.classList.add('active');
  }

  sync.onMessage((msg) => {
    if (msg.type === 'SLIDE_CHANGE' && typeof msg.index === 'number') {
      showSlide(msg.index);
    } else if (msg.type === 'BLANK_TOGGLE') {
      if (blackout) {
        if (msg.active) {
          blackout.classList.add('active');
        } else {
          blackout.classList.remove('active');
        }
      }
    }
  });

  // Local keyboard navigation (if presenting directly without cockpit)
  window.addEventListener('keydown', (e) => {
    if (e.key === 'ArrowRight' || e.key === ' ' || e.key === 'PageDown') {
      showSlide(currentIndex + 1);
      sync.navigate(currentIndex);
    } else if (e.key === 'ArrowLeft' || e.key === 'PageUp') {
      showSlide(currentIndex - 1);
      sync.navigate(currentIndex);
    } else if (e.key.toLowerCase() === 'b') {
      const isBlank = blackout.classList.toggle('active');
      sync.toggleBlank(isBlank);
    }
  });

  // Handle responsive scaling to always keep 16:9 ratio
  function fitViewport() {
    const container = document.querySelector('.deck-container');
    if (!container) return;
    const windowWidth = window.innerWidth;
    const windowHeight = window.innerHeight;
    const targetRatio = 16 / 9;
    const currentRatio = windowWidth / windowHeight;

    let scale;
    if (currentRatio > targetRatio) {
      scale = windowHeight / 720;
    } else {
      scale = windowWidth / 1280;
    }

    container.style.transform = `scale(${scale})`;
    container.style.transformOrigin = 'center center';
  }

  window.addEventListener('resize', fitViewport);
  window.addEventListener('DOMContentLoaded', () => {
    fitViewport();
    showSlide(0);
  });
})();
```

## presenter-controller.js

```javascript
// slidecraft/src/js/presenter-controller.js
(function() {
  const sync = new window.SlideSyncEngine('slidecraft_presentation_channel');
  const slidesData = window.SLIDECRAFT_DATA || [];
  let currentIndex = 0;
  let isBlank = false;
  let timerSeconds = 0;
  let timerInterval = null;

  // DOM Elements
  const timerEl = document.getElementById('timerDisplay');
  const slideCounterEl = document.getElementById('slideCounter');
  const notesContentEl = document.getElementById('notesContent');
  const currentFrame = document.getElementById('currentFrame');
  const nextFrame = document.getElementById('nextFrame');
  const thumbsContainer = document.getElementById('thumbnailsContainer');

  function formatTime(totalSec) {
    const mins = Math.floor(totalSec / 60);
    const secs = totalSec % 60;
    return `${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
  }

  function startTimer() {
    if (timerInterval) return;
    timerInterval = setInterval(() => {
      timerSeconds++;
      if (timerEl) {
        timerEl.textContent = formatTime(timerSeconds);
        // Pacing alert: 20 min mark amber, 25 min mark red
        if (timerSeconds >= 1500) {
          timerEl.className = 'timer-box overtime';
        } else if (timerSeconds >= 1200) {
          timerEl.className = 'timer-box warning';
        }
      }
    }, 1000);
  }

  function pauseTimer() {
    clearInterval(timerInterval);
    timerInterval = null;
  }

  function resetTimer() {
    pauseTimer();
    timerSeconds = 0;
    if (timerEl) {
      timerEl.textContent = '00:00';
      timerEl.className = 'timer-box';
    }
  }

  function renderSlide(index) {
    if (index < 0 || index >= slidesData.length) return;
    currentIndex = index;

    // Update audience via sync
    sync.navigate(currentIndex);

    // Update Counter
    if (slideCounterEl) {
      slideCounterEl.textContent = `${currentIndex + 1} / ${slidesData.length}`;
    }

    // Update Notes
    const slide = slidesData[currentIndex];
    if (notesContentEl) {
      if (slide && slide.notes) {
        // Highlight [STAGE: ...] cues
        let formattedNotes = slide.notes.replace(/\[STAGE:\s*(.*?)\]/gi, '<div class="stage-cue"><strong>🎬 STAGE:</strong> $1</div>');
        notesContentEl.innerHTML = formattedNotes;
      } else {
        notesContentEl.innerHTML = '<span style="color:#64748b; font-style:italic;">No notes provided for this slide.</span>';
      }
    }

    // Update Previews
    if (currentFrame && currentFrame.contentWindow) {
      currentFrame.contentWindow.postMessage({ type: 'GOTO_SLIDE', index: currentIndex }, '*');
    }
    if (nextFrame && nextFrame.contentWindow) {
      nextFrame.contentWindow.postMessage({ type: 'GOTO_SLIDE', index: currentIndex + 1 }, '*');
    }

    // Update active thumb
    document.querySelectorAll('.thumb-card').forEach((card, idx) => {
      if (idx === currentIndex) {
        card.classList.add('active');
        card.scrollIntoView({ behavior: 'smooth', block: 'nearest', inline: 'center' });
      } else {
        card.classList.remove('active');
      }
    });
  }

  function buildThumbnails() {
    if (!thumbsContainer) return;
    thumbsContainer.innerHTML = '';
    slidesData.forEach((s, idx) => {
      const card = document.createElement('div');
      card.className = `thumb-card ${idx === 0 ? 'active' : ''}`;
      card.innerHTML = `
        <div class="thumb-title">${s.meta.title || `Slide ${idx + 1}`}</div>
        <div class="thumb-meta">
          <span>#${idx + 1}</span>
          <span>${s.meta.chapter || ''}</span>
        </div>
      `;
      card.onclick = () => renderSlide(idx);
      thumbsContainer.appendChild(card);
    });
  }

  // Keyboard navigation
  window.addEventListener('keydown', (e) => {
    if (e.key === 'ArrowRight' || e.key === ' ' || e.key === 'PageDown') {
      if (currentIndex < slidesData.length - 1) {
        renderSlide(currentIndex + 1);
      }
    } else if (e.key === 'ArrowLeft' || e.key === 'PageUp') {
      if (currentIndex > 0) {
        renderSlide(currentIndex - 1);
      }
    } else if (e.key.toLowerCase() === 'b') {
      isBlank = !isBlank;
      sync.toggleBlank(isBlank);
    } else if (e.key.toLowerCase() === 't') {
      if (timerInterval) pauseTimer();
      else startTimer();
    } else if (e.key.toLowerCase() === 'r') {
      resetTimer();
    }
  });

  window.addEventListener('DOMContentLoaded', () => {
    buildThumbnails();
    renderSlide(0);
    startTimer();
  });
})();
```

## sync-engine.js

```javascript
// slidecraft/src/js/sync-engine.js
// Sub-50ms window synchronization using BroadcastChannel + localStorage fallback

class SlideSyncEngine {
  constructor(channelName = 'slidecraft_presentation_channel') {
    this.channelName = channelName;
    this.listeners = [];
    this.hasBroadcastChannel = typeof BroadcastChannel !== 'undefined';
    
    if (this.hasBroadcastChannel) {
      try {
        this.bc = new BroadcastChannel(this.channelName);
        this.bc.onmessage = (event) => this.dispatch(event.data);
      } catch (err) {
        console.warn('[SyncEngine] BroadcastChannel failed, using localStorage fallback', err);
        this.hasBroadcastChannel = false;
      }
    }

    // Always wire storage listener as reliable fallback
    window.addEventListener('storage', (event) => {
      if (event.key === this.channelName && event.newValue) {
        try {
          const data = JSON.parse(event.newValue);
          this.dispatch(data);
        } catch (e) {}
      }
    });
  }

  onMessage(callback) {
    this.listeners.push(callback);
  }

  dispatch(message) {
    this.listeners.forEach((fn) => fn(message));
  }

  send(type, payload = {}) {
    const message = {
      type,
      ...payload,
      timestamp: Date.now()
    };

    if (this.hasBroadcastChannel && this.bc) {
      try {
        this.bc.postMessage(message);
      } catch (e) {}
    }

    try {
      localStorage.setItem(this.channelName, JSON.stringify(message));
    } catch (e) {}
  }

  navigate(slideIndex) {
    this.send('SLIDE_CHANGE', { index: slideIndex });
  }

  toggleBlank(active) {
    this.send('BLANK_TOGGLE', { active });
  }

  syncTimer(elapsedSeconds, isRunning) {
    this.send('TIMER_SYNC', { elapsedSeconds, isRunning });
  }
}

if (typeof module !== 'undefined' && module.exports) {
  module.exports = SlideSyncEngine;
} else {
  window.SlideSyncEngine = SlideSyncEngine;
}
```
