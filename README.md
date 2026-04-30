# em-engler-site

A static website for showcasing artwork.

## Project structure

```
public/
  index.html     ← the page
  css/
    styles.css   ← all styling
  img/           ← place for self-hosted image files (contains a .gitkeep so the empty folder is tracked by git)
  pages.html     ← empty placeholder
  comics.html    ← empty placeholder
```

No build step. The browser opens `index.html`, which loads `styles.css`. To work on the site, open `public/index.html` in a browser and refresh after edits.

## HTML overview

[public/index.html](public/index.html) uses semantic tags — `<header>`, `<main>`, `<section>`, `<footer>`, `<nav>` — to describe what each region *is*. Screen readers and search engines rely on these.

The image gallery is a `<div class="image-gallery">` containing `<img>` elements. Each image has:

- `src` — the file location.
- `alt` — text description (used by screen readers and shown if the image fails to load).
- `loading="lazy"` — defers the download until the user scrolls near the image.

## CSS overview

[public/css/styles.css](public/css/styles.css) is ordered:

1. Custom properties (`--color-bg`, `--color-text`) — change colors in one place.
2. Resets — neutralize browser defaults.
3. Base body/typography.
4. Header, main/gallery, footer.
5. Utility class `.link--fader` for hover-fade links.
6. Media queries.

### Mobile-first responsive design

Default rules target the smallest screen. Each `@media (min-width: ...)` block layers additional rules as the viewport grows:

- Default: gallery is 1 column.
- 600px and up: 2 columns.
- 900px and up: 3 columns.

### CSS Grid (the gallery)

`display: grid` plus `grid-template-columns: 1fr 1fr 1fr` produces three equal-width columns. `gap` controls the spacing.

### Units

- `px` — fixed pixels.
- `rem` — relative to the root font size; scales with user accessibility settings.
- `%` — percentage of the parent.
- `fr` — fraction of available space (CSS Grid only).

## Common edits

| Goal | Where |
| --- | --- |
| Change a color sitewide | `:root` variables at top of `styles.css` |
| Add an image | new `<img>` inside `.image-gallery` in `index.html` |
| Add a nav link | new `<li><a class="link--fader" href="...">…</a></li>` in the `<nav>` |
| Change column breakpoints | `min-width` values in the `@media` blocks |
| Apply hover fade to a new link | add `class="link--fader"` |

## Suggested next steps

1. **Write real `alt` text** for each image. Current values are placeholders based on filenames.
2. **Self-host the images.** They currently load from `ekengler.neocities.org`; save them to `public/img/` and update each `src` to `./img/filename.jpg` so the site is self-contained. Once real files exist in `public/img/`, the `.gitkeep` placeholder can be deleted.
3. **Build out `pages.html` and `comics.html`.** Copy the structure from `index.html` and swap the gallery contents.
4. **Add a favicon** (`<link rel="icon" href="...">` in `<head>`).
