# starter-components

Ready-made HTML/JSX scaffolds for slide decks, device frames, window chrome, design canvases, animation rigs, and tweak panels — packaged as a [Claude Code](https://docs.claude.com/en/docs/claude-code) skill so the model copies the right scaffold into your project instead of hand-rolling it.

These components originated in claude.ai's *Make a deck* / design tooling and are vendored here unchanged so they're usable from Claude Code on the desktop. Pair with the [`frontend-design`](https://docs.claude.com/en/docs/claude-code/skills) skill: starter-components gives the structural scaffold; frontend-design gives the aesthetic direction.

## Install

```bash
git clone https://github.com/enstw/starter-components ~/.claude/skills/starter-components
```

Claude Code picks the skill up automatically on next launch — confirm with `/help` or by asking the model what skills it sees.

To uninstall: `rm -rf ~/.claude/skills/starter-components`.

## What's inside

| File | Purpose | Load with |
|---|---|---|
| `deck-stage.js` | Slide-deck shell — 1920×1080 stage, scaling, keyboard nav, slide counter, speaker-notes signaling, print-to-PDF. | `<script src="deck-stage.js"></script>` |
| `design-canvas.jsx` | Pan/zoom canvas for presenting design options side-by-side. Reorderable artboards, inline rename, focus-mode overlay. | `<script type="text/babel" src="design-canvas.jsx"></script>` |
| `ios-frame.jsx` | iPhone device frame — status bar, home indicator, optional keyboard. | `<script type="text/babel" src="ios-frame.jsx"></script>` |
| `android-frame.jsx` | Android device frame — status bar, nav bar, keyboard. | `<script type="text/babel" src="android-frame.jsx"></script>` |
| `macos-window.jsx` | macOS window chrome — traffic lights and titlebar. | `<script type="text/babel" src="macos-window.jsx"></script>` |
| `browser-window.jsx` | Browser window chrome — tabs, URL bar, controls. | `<script type="text/babel" src="browser-window.jsx"></script>` |
| `animations.jsx` | Timeline-based animation engine — Stage, Sprite, easing, scrubber, useTime/useSprite hooks. | `<script type="text/babel" src="animations.jsx"></script>` |
| `tweaks-panel.jsx` | Tweaks shell — host-protocol wiring + form-control helpers (TweakSlider, TweakToggle, TweakColor, etc.). | `<script type="text/babel" src="tweaks-panel.jsx"></script>` |

Each scaffold has a header comment documenting its props and conventions — read it before editing.

## React + Babel setup (for the .jsx files)

The JSX scaffolds expect React 18 + Babel standalone. Use these exact pinned tags:

```html
<script src="https://unpkg.com/react@18.3.1/umd/react.development.js"
  integrity="sha384-hD6/rw4ppMLGNu3tX5cjIb+uRZ7UkRJ6BPkLpg4hAu/6onKUg4lLsHAs9EBPT82L"
  crossorigin="anonymous"></script>
<script src="https://unpkg.com/react-dom@18.3.1/umd/react-dom.development.js"
  integrity="sha384-u6aeetuaXnQ38mYT8rp6sbXaQe3NL9t+IBXmnYxwkUI2Hw4bsp2Wvmx4yRQF1uAm"
  crossorigin="anonymous"></script>
<script src="https://unpkg.com/@babel/standalone@7.29.0/babel.min.js"
  integrity="sha384-m08KidiNqLdpJqLq95G/LEi8Qvjl/xUYll3QILypMoQ65QorJ9Lvtp2RXYGBFj1y"
  crossorigin="anonymous"></script>
```

## Notes

- Keep one copy of `deck-stage.js` per project root, not in a subfolder, so its relative paths work.
- For decks, add a `<script type="application/json" id="speaker-notes">[...]</script>` if you want speaker notes — the deck shell wires it up automatically.
- The JSX components share React scope across files; if you write helpers that need to be available to other JSX files, attach them to `window` at the bottom of the file.
- Each `<script type="text/babel">` gets its own scope when transpiled — don't name shared style objects `styles`; prefix them by component (e.g. `terminalStyles`).

## Layout

```
starter-components/
├── SKILL.md          ← skill manifest Claude Code loads
├── README.md         ← this file
└── assets/           ← scaffolds the skill copies into your project
    ├── deck-stage.js
    ├── design-canvas.jsx
    ├── ios-frame.jsx
    ├── android-frame.jsx
    ├── macos-window.jsx
    ├── browser-window.jsx
    ├── animations.jsx
    └── tweaks-panel.jsx
```
