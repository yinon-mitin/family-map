# Family Map

A small, dependency-free web app for building **family diagrams** (genogram-style "family maps") during therapy, counselling and coaching sessions. Place shapes of different kinds, colours and sizes, connect them with different kinds of lines, then export the result for further discussion.

It is a static site: no build step, no backend, no tracking. It runs on GitHub Pages as-is.

- **Languages:** Russian (default) and English. The choice is remembered per browser.
- **Devices:** desktop (mouse + keyboard) and mobile / tablet (touch, pinch-to-zoom, responsive layout).
- **Privacy:** everything stays in the browser. The diagram is autosaved to `localStorage` on the device and is never uploaded anywhere.

## Features

- **Shapes:** circle, square, triangle, diamond, pentagon, hexagon, star, and free text labels.
- **Appearance:** 13 preset colours plus a custom colour picker, a continuous size slider, filled or outline style, an optional "crossed out" mark (e.g. for a deceased person), and multi-line labels.
- **Links:** solid, dashed, double, zigzag and arrow lines with adjustable colour; arrows can be reversed.
- **Canvas:** drag to move shapes, drag the background to pan, mouse wheel or two-finger pinch to zoom, "fit to screen" button.
- **Editing:** undo / redo (100 steps), duplicate, delete, keyboard nudging.
- **Export:** PNG, SVG, PDF and JSON (a project file you can re-open later). An optional diagram title is printed at the top of exported images and used as the file name.
- **Import:** open a previously exported JSON project.

### Keyboard shortcuts

| Key | Action |
| --- | --- |
| `Delete` / `Backspace` | Delete the selected shape or link |
| `Ctrl/Cmd + Z` | Undo |
| `Ctrl/Cmd + Shift + Z`, `Ctrl/Cmd + Y` | Redo |
| `Ctrl/Cmd + D` | Duplicate the selected shape |
| Arrow keys (`Shift` = bigger step) | Nudge the selected shape |
| `Esc` | Leave link mode / clear selection |
| Double-click a shape | Edit its label |

### How to link two shapes

Either choose the **Link** tool and tap two shapes in turn, or select a shape and press **Link to…** in the properties panel. The line type is taken from the *Line type* group in the toolbar. Tap an existing line (in Select mode) to change its type or colour.

## Running locally

No installation is needed. Any static file server works:

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```

(Opening `index.html` directly from disk also works.)

## Deploying to GitHub Pages

1. Push this repository to GitHub.
2. In **Settings → Pages**, set *Source* to **Deploy from a branch**, choose the `main` branch and the `/ (root)` folder.
3. The site will be available at `https://<user>.github.io/<repository>/`.

## Project structure

```
index.html        page markup (all UI strings are filled in from js/i18n.js)
css/style.css     responsive layout: three-column desktop, bottom-bar mobile
js/i18n.js        Russian and English translations
js/app.js         editor: rendering, interaction, history, export/import
favicon.svg
```

### Adding a language

Add a new object to `window.I18N` in `js/i18n.js` with the same keys as `en`, add an `<option>` to the `#lang` select in `index.html`, and extend the language check in `setLang()` in `js/app.js`.

### Project file format

Exported JSON has the form `{ "app": "family-map", "version": 1, "doc": { "title", "nodes", "links" } }`. Nodes carry `id, shape, x, y, size, color, filled, dead, label`; links carry `id, from, to, style, color`. Imported files are validated and normalised before use.

## Browser support

Current versions of Chrome, Edge, Firefox and Safari (desktop and mobile). The app uses SVG, Pointer Events and the `<dialog>` element.

## License

[MIT](LICENSE)
