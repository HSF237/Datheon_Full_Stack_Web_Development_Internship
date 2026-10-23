# Hasan — Creative Frontend Developer

A single-file personal portfolio with a bold, playful, neo-brutalist look. It introduces Muhammad Hasan, founder of Zerox Studios and Techorbit, and showcases shipped client and personal projects. Plain HTML, CSS and JavaScript: no framework, no build step, no dependencies.

## Highlights

- **Preloader:** a percentage counter that slides away to reveal the page
- **Animated hero:** the name is split into letters that rise in one by one and tilt on hover; a rotating "Available for work" badge; a live Kerala (IST) clock
- **Draggable stickers:** the Student / Freelancer / Founder chips can be dragged around with mouse or touch (Pointer Events)
- **Marquee strip:** an endlessly scrolling tech-stack ticker
- **Scroll reveals:** sections fade in and highlighter marks sweep across key phrases, using `IntersectionObserver`
- **Skills list:** four grouped rows that invert colours on hover
- **Project list:** filter by All / Client work / Personal, with a live count line
  - On desktop, hovering a project shows a floating coloured preview tile that follows the cursor with easing
  - Clicking opens a native `<dialog>` modal with description, role, status, highlights, tech tags, live link and optional GitHub link, plus Prev / Next navigation
- **Journey section:** sticky, slightly rotated cards that stack as you scroll
- **Contact block:** email, WhatsApp, GitHub and LinkedIn links
- **Theme toggle:** light and dark, remembered in `localStorage` and defaulting to your system setting
- **Mobile menu:** a full-screen sliding nav under 820px
- **Custom cursor** for mouse users only

## Accessibility and robustness

- Respects `prefers-reduced-motion` (skips the preloader and custom cursor)
- Custom cursor and hover preview are removed on touch devices
- `<noscript>` fallback keeps content visible without JavaScript
- Semantic landmarks, labelled buttons, `aria-expanded` on the menu, native dialog focus handling
- Safe-area insets for notched phones
- Storage access wrapped in `try/catch`

## Getting started

1. Save the file as `index.html`.
2. Open it in a browser, or serve the folder with any static host.
3. Put your résumé next to it as `resume.pdf`. The "Download résumé" button links to that filename, so it will 404 until the file exists.

## Deploying

It is one static file, so it works on GitHub Pages, Vercel, Netlify or any web server. Fonts load from Google Fonts, so the page needs internet access for its typefaces; it falls back to Helvetica/Arial and Georgia otherwise.

## Content map

| Section | Contents |
|---|---|
| 01 About | Intro paragraph and an ID card |
| 02 Skills | Frontend, Backend & data, Motion & 3D, Workflow |
| 03 Selected work | Six featured projects |
| 04 Résumé | Zerox Studios, VEloop Rewards internship, Techorbit |
| 05 Contact | Email and social links |

### Featured projects

| Project | Type | Stack |
|---|---|---|
| Meridian Arch Studio | Client work | React, Node.js, JavaScript |
| Al Awaans Online Shop (formerly Leens) | Client work | React, Node.js, JavaScript |
| TISK EMS | Client work | Web, responsive design |
| Sol Harbor | Personal project | Three.js, JavaScript, GitHub Pages |
| AI Finder | Personal project | Web |
| Elite Engine | Client work | Vercel, Web |

## Customising

All content lives in the `<script>` block as data, so you rarely touch the markup.

- **Skills:** edit the `SK` array.
- **Projects:** edit `PJ` (name, type, URL, stack, short description, colour, initials) and `DT` (tagline, role, status, highlights, optional `g` GitHub link). The two arrays are merged **by index**, so keep them in the same order. Adding a project means adding an entry to both.
- **Marquee words:** edit the list in the `tk` variable.
- **Journey, About, ID card, contact links:** edit the HTML directly.
- **Colours:** change the CSS variables at the top of the stylesheet (`--bg`, `--ink`, `--card`, `--o`, `--y`, `--m`) and the dark-mode values beneath them.
- **Fonts:** Bricolage Grotesque and Instrument Serif, set by `--f` and `--s`.
- **Clock time zone:** change `Asia/Kolkata` in the `tick()` function.

## Tech

HTML5, CSS3 (custom properties, grid, flexbox, `clamp()`, sticky positioning, `@media` queries), vanilla JavaScript (ES5 style, wrapped in an IIFE), Pointer Events, IntersectionObserver, the `<dialog>` element.

## Contact

- Email: zerox9861@gmail.com
- GitHub: [HSF237](https://github.com/HSF237)
- LinkedIn: [muhammad-hasan](https://linkedin.com/in/muhammad-hasan-b138283b7)

© Muhammad Hasan. Made in Kerala with code and chai.
