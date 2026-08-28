# Voltbook — responsive client website

CSS group assignment — responsive client website.

**Voltbook** is our imaginary company: a small laptop shop that grew out of a
repair workshop and only sells machines its own technicians are happy to use.
Target audience: developers, designers and students who want a reliable laptop
without the upsells.

## Pages

| Page | File | Notes |
|------|------|-------|
| Home / landing | `index.html` | Built to the client's rough design (hero, info boxes, quote, call-to-action). |
| Products | `products.html` | The four-laptop range as flexbox cards. |
| About | `about.html` | Company story, stats band, team. |
| Contact | `contact.html` | Contact details + a semantic form, repair-centre list. |

All pages share the same `<header>` navigation, `<footer>` and `styles.css`.

## Running it

It is plain static HTML/CSS — open `index.html` in a browser, or serve the
folder:

```bash
python -m http.server 8000
# then visit http://localhost:8000
```

## Technical checklist

- **Semantic HTML** — `header`, `nav`, `main`, `section`, `article`, `figure`/
  `figcaption`, `blockquote`, `footer`, a labelled `form`.
- **Vanilla CSS**, one external stylesheet (`styles.css`).
- **Flexbox** for every layout. **No CSS Grid anywhere.**
- **Media queries** at `900px` (tablet → burger menu, columns stack) and
  `600px` (phones → single column, tighter spacing).
- **Roboto** imported at the top of `styles.css` with `@import` from Google
  Fonts (weights 300 / 400 / 500 / 700 / 800 / 900 + 300 italic).
- **CSS-only burger menu** — no JavaScript (see below).
- **Font Awesome** — used only for icons (feature bullets, footer socials,
  contact details).
- **No JavaScript at all.**

### Typography & colours (from the client's style sheet)

| Element | Size | Weight | Colour |
|---------|------|--------|--------|
| Dark background (hero, footer) | — | — | `#1F2937` |
| Hero main heading | 48px (`clamp` down to 32px) | 800 extra-bold | `#F9FAF8` |
| Hero sub-text / header links | 18px | 400 | `#E5E7EB` |
| Header logo | 24px | 700 | `#F9FAF8` |
| Info / section heading | 36px (`clamp` down to 28px) | 800 extra-bold | `#1F2937` |
| Button / call-to-action background | — | — | `#3882F6` |
| Quote section background | — | — | `#E5E7EB` |
| Quote text | 36px (`clamp` down to ~22px) | 300 light italic | `#1F2937` |

Desktop sizes match the spec exactly; `clamp()` only shrinks them on narrow
screens so headings never overflow.

## Responsive images — which technique, and why

Four different techniques, one per use case:

1. **Hero image — `<picture>` with `<source media>` (art direction).**
   `index.html` swaps a wide 16:9 crop for a taller 4:5 crop below 700px, so on
   a phone the laptop stays large instead of becoming a thin strip beside the
   heading. Inside each `<source>`, `srcset` + `sizes` still let the browser
   pick the right resolution.

2. **Product cards, team photos, story images — `srcset` + `sizes` (resolution
   switching).** Same picture, just needed at different pixel sizes. The browser
   compares `sizes` (e.g. `(max-width: 600px) 90vw, 300px`) against the
   viewport and device pixel ratio and downloads the smallest file that still
   looks sharp. No art direction needed — the crop is fine at every size.

3. **Decorative pattern band — CSS `background-image` + media query.**
   The diagonal pattern behind the "Voltbook today" / "repair centres" bands is
   purely decorative, so it does not belong in the HTML. A media query serves
   `pattern-900.jpg` to phones and `pattern-1800.jpg` only above 900px, so small
   screens never download the large file.

4. **Every content image also has `width`/`height` attributes** (to reserve
   space and avoid layout shift) and is capped with `max-width: 100%; height:
   auto; object-fit: cover`, so images always fit their container without
   stretching or distorting.

## CSS-only burger menu — how it works

We first tried the **`:target`** approach (a link to `#nav`, opened with
`nav:target`). It works, but clicking the burger makes the browser scroll the
target to the top of the viewport, which pushes the header off-screen.

We switched to the **checkbox technique**:

```html
<input type="checkbox" id="nav-toggle" class="nav-checkbox" />
<label for="nav-toggle" class="nav-toggle"><span></span>…</label>
<nav class="main-nav"> … </nav>
```

- The `<label>` is tied to the hidden `<input type="checkbox">` by `for`/`id`,
  so clicking the label toggles the checkbox — no script needed.
- The checkbox and the `<nav>` are siblings, so
  `.nav-checkbox:checked ~ .main-nav { max-height: 320px; }` opens the panel
  (it animates from `max-height: 0`).
- The same `:checked` state rotates the three `<span>` bars into an X.
- On screens wider than 900px the label is `display: none` and the nav is shown
  normally, so the checkbox has no effect.

The checkbox keeps its own state, so there is no scroll jump, and clicking the
burger a second time closes the menu.

<<<<<<< HEAD
## Where we used AI (Think → Try → Ask AI → Understand → Test → Accept/Modify/Reject)

1. **Ideation.** After picking "laptop shop", we asked AI to expand the concept
   (name, audience, page list, section content) and trimmed its suggestions to
   four pages.
2. **Concept — burger menu.** We asked AI to *explain* the CSS-only options
   (`:target` vs checkbox vs `:focus-within`), understood the trade-offs
   ourselves, then chose the checkbox method and tested it at 375 / 768 / 1200.
3. **Concept — responsive images.** We asked AI when to use `<picture>` vs
   `srcset`/`sizes` vs a CSS background, then mapped each image on the site to
   the technique that fit its purpose (see above).
4. **Review.** Near the end we asked AI to review the HTML/CSS for spec
   compliance, horizontal overflow and accessibility. Accepted: adding
   `min-width: 0` to flex items to stop an image overflowing, `height: auto` on
   images, a dark wash over the decorative pattern for contrast. Rejected:
   suggestions that would have needed JavaScript or CSS Grid.
=======
## Responsive strategy

Tested at 375px (mobile), 768px (tablet) and 1200px+ (desktop):

- Below 900px the desktop nav is replaced by the burger menu, and the hero and
  "split" sections stack from two columns into one.
- Below 600px the feature/product/team rows collapse to a single column and
  spacing tightens.
- No element overflows horizontally at any width; images are capped with
  `max-width: 100%` and `object-fit: cover` so they never stretch.
>>>>>>> 1e12fd71b5fb230d4a6ac85e937922bbb7f4776f

## Team

Built collaboratively on GitHub. Commits are attributed to each member.
