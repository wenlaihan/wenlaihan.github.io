# wenlaihan.github.io

Personal research website for Wenlai Han — live at <https://wenlaihan.github.io/>.

Plain HTML and CSS with no build step, no dependencies, and no JavaScript. GitHub Pages
serves `main` directly, so pushing to `main` publishes the site.

```
index.html     the whole site
styles.css     the whole stylesheet (light + dark, follows the visitor's system setting)
404.html       not-found page
assets/        cv.pdf, favicon.svg, and photo.jpg once you add it
.nojekyll      skips the Jekyll build on GitHub Pages
```

## Preview locally

```sh
python3 -m http.server 8000    # then open http://localhost:8000
```

## Adding a headshot

Until a photo exists the hero shows a "WH" monogram, which is a finished-looking
placeholder rather than a gap.

1. Save a square crop (600×600 or larger, under ~300 KB) as `assets/photo.jpg`.
2. In `index.html`, replace the whole `<figure class="headshot">` block with

   ```html
   <div class="headshot">
     <img src="assets/photo.jpg" alt="" width="600" height="600" decoding="async">
   </div>
   ```

   Use `alt=""`, not a description: the name is already the `<h1>`, so an accessible
   name here would only make screen readers say it twice. Dropping the `<figure>` and
   its `aria-hidden` at the same time avoids two traps — `aria-hidden` would silently
   suppress any alt text, and it becomes an outright error if the portrait is ever
   wrapped in a link.
3. Optionally add `<meta property="og:image" content="https://wenlaihan.github.io/assets/photo.jpg">`
   to `<head>` so link previews show the photo.

No CSS changes are needed — the image inherits the monogram's size and rounding, and
`object-fit: cover` centre-crops whatever aspect ratio you supply.

## Updating the CV

Export the current CV over `assets/cv.pdf`, keeping the filename. The link in
`index.html` never has to change.

## Conventions worth keeping

- Colors live as custom properties at the top of `styles.css`; the dark theme redefines
  only those tokens. Never hard-code a color further down the file.
- Filenames stay lowercase — GitHub Pages URLs are case-sensitive even though macOS
  filenames are not.
- Publication entries link their title to the DOI, bold `Han, W.`, and mark equal
  contribution with `†`.
