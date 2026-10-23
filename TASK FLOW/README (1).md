# Taskflow

A clean, animated task manager in a single HTML file. No server, no build step, no dependencies. Tasks and filters are saved to the browser the moment they change.

## Features

- **Add tasks with a category** (Work, Personal, Shopping, Health, Learning). New tasks appear at the top.
- **Animated completion.** The checkmark draws itself, the text is struck through, a ripple ring fades out, and the progress ring in the header updates.
- **Drag-and-drop reordering** with the grip handle. Works with mouse, touch and pen, and also from the keyboard.
- **Live search** across task text and category names.
- **Filter toggles:** an All / Active / Done switch with counts, plus multi-select category chips with counts.
- **Inline editing.** Click a task to edit it. Click its category tag to cycle the category.
- **Undo** for deleting a task and for clearing completed tasks.
- **Responsive** down to phone widths, with light and dark themes that follow the system setting.
- **Accessible motion.** Animations are skipped when the system asks for reduced motion.

## Quick start

Open `taskflow.html` in a modern browser. To serve it locally instead (the most reliable way to get persistent storage):

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/taskflow.html
```

## Keyboard shortcuts

| Key | Action |
| --- | --- |
| `Enter` in the input | Add the task |
| `/` | Focus the search box |
| `Esc` in search | Clear the search and leave the box |
| `Enter` on a focused task | Start editing |
| `Enter` while editing | Save the edit |
| `Esc` while editing | Cancel the edit |
| `Up` / `Down` on a focused grip | Move the task one place |

## How data is stored

State lives in a plain array, `tasks = []`, and is written to `localStorage` after every change by `saveToLocalStorage()`. `loadFromLocalStorage()` restores it on startup. If nothing is stored yet, five sample tasks are created.

Storage key: `taskflow.v1`

```json
{
  "tasks": [{ "id": "k3j9x2ab", "text": "Book a dentist appointment", "cat": "health", "done": true }],
  "ui": { "status": "all", "cats": [], "cur": "work" }
}
```

What survives a reload: tasks, their order and completed state, the status toggle, the category filters, and the category selected for new tasks. The search text is not saved.

To reset everything, run this in the browser console:

```js
localStorage.removeItem('taskflow.v1'); location.reload();
```

## How it works

The file has three parts: a `<style>` block (design tokens first), the markup, and one script.

- `match(task)` is the filter predicate shared by the status toggle, category chips and search.
- `render()` reconciles the list by task id, so existing items are reused rather than rebuilt. It animates entering, leaving and moving items using the Web Animations API (a FLIP technique).
- `toggle()`, `remove()` and `edit()` change a task, save, and re-render.
- Drag-and-drop uses pointer events. Other items slide aside while you drag, and the new order is written back into `tasks` on drop. This works even when filters hide some tasks.
- Adding a task that the current filters would hide resets the filters so the new task is visible.

## Customizing

**Categories.** Edit the `CATS` array in the script, then define a matching `--c-<id>` color in all three token blocks at the top of the stylesheet (light, dark via media query, and `[data-theme=dark]`). Tasks whose category no longer exists fall back to the first category.

**Theme.** The page follows the system light or dark setting. To force one, set `data-theme="light"` or `data-theme="dark"` on the `<html>` element.

**Data format changes.** If you change the saved structure, bump the `taskflow.v1` key so old data is not read in the new shape.

## Browser support

Current versions of Chrome, Edge, Safari and Firefox. The page uses pointer events, the Web Animations API and CSS `color-mix()` (tinted tags fall back to a neutral tint where it is missing).

## Limitations

- Data is per browser and per device. There is no sync or account.
- Clearing site data deletes your tasks, and private or incognito windows usually discard them when closed.
- If the browser blocks storage, the app still works but forgets everything on reload.
- An edit that has not been confirmed (Enter or clicking away) is lost on reload.

## Deploying

Taskflow is a static file. Rename it to `index.html` and upload it to any static host (GitHub Pages, Netlify, Vercel, an S3 bucket). No configuration is needed.
