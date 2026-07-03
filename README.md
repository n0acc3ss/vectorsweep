# Vector Sweep

<img src="https://i.ibb.co/HLmzdwdg/logo-vector-sweep.webp" align="center">
Find & replace and optimize across thousands of SVG files — entirely in your browser, no upload, no server, no build step.

Vector Sweep is a single-page, single-file web app that lets you point at a local folder of `.svg` icons and batch-recolor, find-and-replace, or strip cruft from every file in it. Everything runs client-side using the [File System Access API](https://developer.mozilla.org/en-US/docs/Web/API/File_System_Access_API) — your files never leave your machine.

**[Live app: → https://n0acc3ss.github.io/vectorsweep/](https://n0acc3ss.github.io/vectorsweep/)**``

## Features

- **Folder picker, not file uploads** — grants direct read/write access to a local directory via the browser's native folder picker.
- **Configurable recursion** — process just the top folder, all subfolders, or a fixed depth, filtered by file extension (defaults to `svg`).
- **Auto-recolor to solid** — detects every way an SVG can carry color (`fill`/`stroke` attributes, inline `style`, internal `<style>` rules, gradient/pattern fills) and rewrites them all to one color (black, white, or `currentColor`), while leaving `fill="none"` and `<mask>`/`<clipPath>` luminance untouched.
- **Manual find & replace** — plain-text or regex matching, case-sensitive toggle, applied across every matched file.
- **Live preview** — test your color or replace rule against a sample SVG, rendered on light and dark tiles, before touching real files.
- **Optimize / minify** — optional cleanup pass that strips XML declarations, DOCTYPEs, comments, `<metadata>`, Inkscape/Illustrator editor namespaces, and collapses whitespace. Removing the root `xmlns` is available but flagged as unsafe unless icons are inlined in HTML.
- **Flexible save modes** — overwrite files in place, save copies with a filename suffix, or write the whole processed tree into a new output folder, leaving originals untouched.
- **Live console** — scan/match/write counters, a progress bar, and a scrollable log you can clear or export as a text file.

## Usage

1. Open the app in **Chrome or Edge on desktop** (the File System Access API isn't available elsewhere, and it must be opened in a full tab, not an iframe).
2. **Select a folder** of SVGs.
3. Choose **recursion depth** and file extensions.
4. Pick **Recolor to solid** or set up a **manual find & replace** (with optional regex), and sanity-check it in the live preview.
5. Optionally enable **Optimize** and choose which cleanup steps to apply.
6. Choose a **save mode** — replace originals, save suffixed copies, or write to a new folder.
7. Click **Preview** to dry-run and see match counts, or **Run** to process the files. Replacing originals asks for confirmation first — there's no undo.

## Browser support

Requires a browser implementing `window.showDirectoryPicker` (Chromium-based desktop browsers — Chrome, Edge, etc.). The app detects support on load and shows a status pill in the header.

## Running locally

No build tooling, dependencies, or install step — it's a single `index.html`.

```bash
git clone https://github.com/n0acc3ss/vectorsweep.git
cd vectorsweep
python3 -m http.server 8000
# open http://localhost:8000
```

(A local server is only needed because some browsers restrict the File System Access API on `file://` URLs.)

## Deployment

Pushes to `main` are published to GitHub Pages via `.github/workflows/static.yml`.

## License

[GPL-3.0](LICENSE)
