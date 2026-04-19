# cindy-web
A web-based editor for [CindyJS](https://cindyjs.org/) — write, run, and export CindyScript directly in the browser.

## Features

- **Tabbed script editor** with syntax highlighting (CodeMirror + Dracula theme) for all CindyJS event slots: `init`, `draw`, `tick`, `mousemove`, `mousedown`, `mousedrag`, `mouseup`
- **Live preview** on a resizable canvas panel beside the editor
- **Optional module imports**: Animation, UI, Color, 3D Camera
- **Prefill support** — load starter code via URL parameter (`?prefill=animationBoilerplate`)
- **Persistent state** — editor contents and import selections are saved to `localStorage` and restored on reload
- **Export** — download your sketch as:
  - a single self-contained HTML file with all scripts inlined, or
  - a ZIP package with `.cjs` files + `config.json` (optionally including imported packages and `Cindy.js`)
- **Keyboard shortcuts**: `Ctrl/Cmd+Enter` to run, `Ctrl/Cmd+S` to save
- **Resizable panels** — drag the column and row dividers to adjust editor, console, and canvas sizes

## Setup

This editor expects `Cindy.js` (and optionally package folders like `animation/`, `ui/`, `color.cjs`, `camera.cjs`) to live one directory above `cindy-web/`. A typical layout:

```
parent/
├── Cindy.js
├── animation/
├── ui/
├── color.cjs
├── camera.cjs
└── cindy-web/
    ├── editor.html
    ├── editor.js
    ├── editor.css
    └── prefills/
```

Open `editor.html` via a local web server (e.g. `npx serve .` or `python -m http.server` or VS Code Live Server). Opening it directly as a `file://` URL will block `fetch()` calls used for prefills and exports.

## URL Parameters

| Parameter | Description |
|-----------|-------------|
| `?prefill=<name>` | Load starter scripts from `prefills/<name>/` on first open |
| `?animation`, `?ui`, `?color`, `?camera` | Pre-check the corresponding import checkbox |

Example: `editor.html?prefill=animationBoilerplate&animation`

## Prefills

Each prefill is a folder under `prefills/` containing one `.cjs` file per script slot (only non-empty slots need a file):

```
prefills/
└── animationBoilerplate/
    ├── init.cjs
    ├── draw.cjs
    ├── tick.cjs
    └── ...
```

## Export formats

**Single file** — all scripts and (optionally) `Cindy.js` are bundled into one standalone HTML file.

**Packaged ZIP** — scripts are saved as `.cjs` files with a `config.json` manifest, ready to be consumed by the CindyJS package loader. Selected imported packages can be included in the ZIP.

## License

See [LICENSE](LICENSE).
