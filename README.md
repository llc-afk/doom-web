# doom-web

Doom in a browser page — the Chocolate Doom engine compiled to WebAssembly,
running the Freedoom game data. Everything is served from this repository via
GitHub Pages; the page fetches nothing from anywhere else.

Open it, tap **TAP TO START**, and play. The game fills the browser viewport and
requests fullscreen when the browser allows it. The **MAPAS** button in the
in-game toolbar opens one menu with every campaign and map; changing either
reloads directly into the selected level. On a fresh visit, the normal Doom
title menu remains available. On touch screens, the controls overlay the game
and can be collapsed with the controls button in the top-right corner. A
keyboard works too (arrows to move and turn,
A / D to strafe, Ctrl to fire, Space to open doors, Shift to run, number keys
to switch weapons). Click the game view to capture the mouse for aiming; use
the fullscreen button in the top-right corner to enter or leave fullscreen.

First load pulls about 41 MB, including the optional episode packs. After that
the browser cache serves the files.

## Extra Doom 1 episodes

The in-game map menu lets you choose between Freedoom's campaign and three
additional Episode 1 replacements: **Simply Phobos** (Paul Corfiatis and
Kristian Aro), **Doom: Awesome, Episode 1** (Giest118), and **Phobos Revisited**
(ReX Claussen). They run on the included Freedoom IWAD. The Simply Phobos
archive also includes its optional music WAD; music remains disabled in this
browser build. Its extra E2M9 map requires a limit-removing port, while its E1
episode runs with Chocolate Doom.

Each WAD is distributed with its original author-provided text file, as the
authors' permissions require. Those text files are kept unmodified beside the
WADs in `maps/`.

The browser output is configured for 800×600, with smooth scaling enabled. The
Chocolate Doom engine still draws the original game scene at 320×200 before
upscaling it, so this smooths the enlarged pixels but does not create new detail
in the original art. Simply Phobos's E2M9 appears in the map list but may need a
limit-removing source port, as noted by its authors.

---

## What is in here, and who owns it

This repository contains two independently licensed things. They are kept
separate on purpose.

### The engine — GPLv2

| File | What |
|---|---|
| `websockets-doom.wasm` | Chocolate Doom compiled to WebAssembly |
| `websockets-doom.js` | Emscripten loader/glue for the above |

id Software released the Doom engine source under the GNU GPL v2, and Chocolate
Doom inherits that license. The full license text is in [`COPYING`](COPYING).

**Corresponding source.** These binaries are unmodified build artifacts. They
were taken from the published GitHub Pages deployment of:

- Deployment commit: `Saketh-Chandra/doom-wasm-pwa@5b1e1fe7385b6f0b19d60dece6adbf88f6842e20` (branch `gh-pages`, 2023-03-09)
- Built from source revision: `Saketh-Chandra/doom-wasm-pwa@a77edfd8bbc7`
- Which is a fork of: <https://github.com/cloudflare/doom-wasm> (declared GPL-2.0)
- Which is a WebAssembly port of: <https://github.com/chocolate-doom/chocolate-doom>

The complete corresponding source for these binaries is the tree at
`Saketh-Chandra/doom-wasm-pwa@a77edfd8bbc7`, publicly available at the URL above.

No modifications were made to the engine binaries. The browser launcher and
presentation are in `index.html`; `default.cfg` and `chocolate-doom.cfg` contain
game and display settings.

### The game data — BSD 3-clause

| File | What |
|---|---|
| `freedoom1.wad` | Freedoom: Phase 1 game data (v0.13.0) |
| `FREEDOOM-COPYING.txt` | Freedoom's BSD 3-clause license |
| `FREEDOOM-CREDITS.txt` | Freedoom contributor credits |

[Freedoom](https://freedoom.github.io/) is a free-content replacement for Doom's
game assets — original levels, sprites, sounds, and music, written from scratch.
It contains **no id Software content**. Taken unmodified from the official
`freedoom-0.13.0.zip` release.

`freedoom1.wad` here is a valid IWAD: 3163 lumps, 27.5 MB.

### The page — `index.html`

Original. Loads the engine, pulls `freedoom1.wad` into the emscripten virtual
filesystem before `main()` runs, and adds a touch control layer that synthesizes
keyboard events. Written for this repository.

---

## What is deliberately not here

No `doom1.wad`, `doom.wad`, or `doom2.wad`. Those are id Software's copyrighted
game data and are not redistributable. Freedoom exists precisely so that none of
them are needed.

---

## Running it locally

```bash
python3 -m http.server 8080
```

Then open <http://localhost:8080>. Any static file server works — there is no
build step and no backend.
