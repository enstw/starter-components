---
name: starter-components
description: Copy ready-made scaffolds for slide decks, device frames, window chrome, design canvases, animations, and tweak panels instead of hand-rolling them.
---

When the user asks for a slide deck, prototype, animated video, side-by-side
design comparison, or a tweakable design, copy the matching scaffold from
`~/.claude/skills/starter-components/assets/` into the project root before
writing the design. Always copy — never reference from the skill's assets
folder — so the project stays self-contained.

Read the copied file before using it. Each scaffold has a header comment
documenting its props and conventions.

Pair with the `frontend-design` skill: starter-components gives structural
scaffolds; frontend-design gives aesthetic direction.

## Available scaffolds

| File | Purpose | Load with |
|---|---|---|
| `deck-stage.js` | Slide-deck shell — 1920×1080 stage, scaling, keyboard nav, slide counter, speaker-notes signaling, print-to-PDF. Each slide is a `<section>` child of `<deck-stage width="1920" height="1080">`. | `<script src="deck-stage.js"></script>` |
| `design-canvas.jsx` | Pan/zoom canvas for presenting design options side-by-side. Reorderable artboards, inline rename, focus-mode overlay. Wrap variations in `<DCArtboard>` inside `<DCSection>`. | `<script type="text/babel" src="design-canvas.jsx"></script>` |
| `ios-frame.jsx` | iPhone device frame — status bar, home indicator, optional keyboard. | `<script type="text/babel" src="ios-frame.jsx"></script>` |
| `android-frame.jsx` | Android device frame — status bar, nav bar, keyboard. | `<script type="text/babel" src="android-frame.jsx"></script>` |
| `macos-window.jsx` | macOS window chrome — traffic lights and titlebar. | `<script type="text/babel" src="macos-window.jsx"></script>` |
| `browser-window.jsx` | Browser window chrome — tabs, URL bar, controls. | `<script type="text/babel" src="browser-window.jsx"></script>` |
| `animations.jsx` | Timeline-based animation engine — Stage, Sprite, easing, scrubber, useTime/useSprite hooks. | `<script type="text/babel" src="animations.jsx"></script>` |
| `tweaks-panel.jsx` | Tweaks shell — host-protocol wiring + form-control helpers (TweakSlider, TweakToggle, TweakColor, etc.). | `<script type="text/babel" src="tweaks-panel.jsx"></script>` |

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
