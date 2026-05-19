# darkmatter-manchester.github.io

Source for the Dark Matter Manchester group website, served via GitHub Pages
at **<https://darkmatter-manchester.github.io>**.

## Editing content

The site is plain HTML/CSS — no build step, no Jekyll, no dependencies. To
change content:

1. Open `index.html` in any editor.
2. Look for `<!-- EDIT ME -->` comments and the obvious placeholders
   (`[surname]`, paper titles, email addresses).
3. Update sections as needed. The HTML is structured so each part of the
   page (hero, about, research themes, people, publications, contact) is
   clearly demarcated.
4. Commit and push to `main`. GitHub Pages will rebuild and deploy the
   site within a minute or two.

## Editing styles

All visual design is controlled by `styles.css`. The most impactful
parameters are at the top of the file in the `:root` block: colours,
fonts, spacing. Change a couple of CSS variables to retheme the site
without touching the rest.

## Adding new pages

For a single new page (e.g. an outreach page or a longer research
description):

1. Create e.g. `outreach.html` alongside `index.html`. Easiest is to copy
   `index.html` and gut the body, keeping the `<head>`, header, and footer
   for visual consistency.
2. Add a link to it from `index.html`'s navigation.

If the site grows beyond a handful of pages, consider switching to a
static-site generator (Jekyll, Hugo, Eleventy). Jekyll is auto-supported
by GitHub Pages and would let collaborators write content in Markdown.

## Local preview

No build step is required. To preview locally, either:

- Open `index.html` directly in a browser; or
- Run a simple HTTP server in the repo root, e.g.
  `python -m http.server 8080`, then visit <http://localhost:8080>.

## Deployment

GitHub Pages is configured automatically for repositories named
`<org>.github.io`. To verify or change settings:

1. Go to the repository on GitHub.
2. *Settings → Pages*.
3. Source should be `Deploy from a branch`, branch `main`, folder `/ (root)`.

For a custom domain (e.g. `darkmatter.manchester.ac.uk`), add a `CNAME`
file containing the domain and configure DNS records as instructed by
GitHub.

## License

Site content (text, images authored by group members) is © Dark Matter
Manchester, University of Manchester. The site template (HTML and CSS
structure) is released under the MIT License — see `LICENSE`.
