# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This repository contains two standalone single-file HTML applications written in Japanese:

- **dq2.html** — A Dragon Quest II–style browser RPG game rendered on an HTML5 `<canvas>`. All game logic (input, map, battle, UI) is self-contained in one file with no external dependencies.
- **hospital-wiki.html** — A hospital internal rules management system (院内ルール管理システム). A single-page wiki/document viewer with sidebar navigation, search, and a rule editor, also fully self-contained.

## Development

No build step, package manager, or test suite is used. Open either `.html` file directly in a browser to run it.

To preview changes quickly:

```bash
# Any local HTTP server works, e.g.:
python3 -m http.server 8080
# Then open http://localhost:8080/dq2.html or http://localhost:8080/hospital-wiki.html
```

## Architecture

### dq2.html

- Single `<canvas id="game">` element driven by a `requestAnimationFrame` game loop.
- **Input**: keyboard events (`keydown`/`keyup`) and touch/mouse events on the on-screen D-pad buttons are unified into `keys` (held state) and `pressed` (edge-triggered) maps.
- **Game loop**: calls `update()` then `draw()` each frame; a `delta` accumulator drives fixed-step movement.
- **Scenes**: controlled by a `scene` variable (`'title'`, `'world'`, `'dungeon'`, `'battle'`, `'menu'`, etc.); each scene has its own update and draw branch.
- **Rendering**: all graphics are drawn programmatically with Canvas 2D API using pixel-art tile drawing helpers; no image assets are used.

### hospital-wiki.html

- Single-page application with no framework; all state is held in JS variables in the `<script>` block.
- **Sidebar**: category sections rendered from a `DATA` object; clicking items renders the corresponding rule article in the main content area.
- **Search**: filters sidebar items and highlights matches in real time using plain DOM manipulation.
- **Editor**: inline rule editing UI toggled by an edit button; changes are stored only in memory (no backend/localStorage persistence by default).
- **Responsive**: a hamburger menu and overlay handle mobile sidebar toggling via CSS classes.
