# room-site

A small personal-site template inspired by "clickable room" homepages
(like [ribo.zone](https://ribo.zone)) — an illustrated scene where
each object is a link, built with plain HTML and CSS. No build step,
no framework, no JavaScript required.

## Live preview

Open `index.html` directly in a browser, or serve the folder locally:

```bash
# Python
python3 -m http.server 8000

# Node (if you have it)
npx serve .
```

Then visit `http://localhost:8000`.

## Structure

```
room-site/
├── index.html       the homepage — the clickable room
├── about.html        example content page
├── projects.html      example content page
├── contact.html       example content page
├── secret.html        example "hidden" page (linked from a fade-in object)
├── 404.html            shown for broken links on GitHub Pages
├── style.css           all shared styles
├── images/              put your scene + object PNGs here
├── LICENSE
└── .gitignore
```

## How the room works

`index.html` has a `.room` container with a fixed `aspect-ratio`. Every
clickable object inside it is an `<a>` (or `<button>`, for the popover
example) positioned with `top` / `left` / `width` percentages, so the
whole scene scales responsively without breaking the layout.

Two hover styles are included, set via class name:

- **`.thing.rotate`** — the object tilts slightly and a text label
  fades in. Good for most objects.
- **`.thing.appear`** — the object itself is invisible (or faint)
  until hovered, then fades in. Good for hidden "secret" objects.

## Adding your own art

1. Draw or commission one flat image of your scene (a room, desk,
   garden, etc). Save it in `images/`.
2. Set it as the room's background in `style.css`:
   ```css
   .room {
     background: url('images/scene.png');
   }
   ```
   and update `aspect-ratio` to match your image's actual proportions.
3. For each clickable object, cut out a separate transparent PNG at
   the same resolution as the full scene.
4. In `index.html`, replace `<div class="placeholder"></div>` with
   `<img src="images/your-object.png" alt="">` for each object.
5. Work out each object's position as a percentage of the full image:
   ```
   top%   = (object's y position in px) / (scene height in px) * 100
   left%  = (object's x position in px) / (scene width in px)  * 100
   width% = (object's width in px)      / (scene width in px)  * 100
   ```

## Adding a new page

Copy `about.html`, rename it, edit the content inside `<main class="page">`,
and add a new object on `index.html` (or a link in the `<nav>`) pointing
to it.

## Deploying to GitHub Pages

1. Push this repo to GitHub.
2. Go to **Settings → Pages**.
3. Under "Build and deployment", set **Source** to "Deploy from a branch",
   pick the `main` branch and `/ (root)` folder, then save.
4. Your site will be live at `https://<username>.github.io/<repo-name>/`
   within a minute or two.

## Credit

Layout technique inspired by the "clickable room" style of homepage,
as seen on sites like [ribo.zone](https://ribo.zone).
