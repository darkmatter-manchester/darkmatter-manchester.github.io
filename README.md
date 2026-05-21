# darkmatter-manchester.github.io

Source for the Dark Matter Manchester group website, served via GitHub
Pages at **<https://darkmatter-manchester.github.io>**.

Built with **Jekyll**, auto-deployed by GitHub Pages. Content lives in
plain text files: HTML and Markdown for page structure, YAML for
repeatable content (people, publications, etc.). No JS build step,
no node, no front-end framework.

---

## Repository layout

```
.
├── _config.yml              ← Jekyll configuration & site metadata
├── Gemfile                  ← Ruby dependencies (for local preview)
├── .gitignore
│
├── _layouts/
│   ├── default.html         ← Wraps every page (head + header + footer)
│   ├── theme.html           ← Research theme pages (breadcrumb, figure, body)
│   └── subpage.html         ← Generic sub-page (breadcrumb, hero, body) — Join pages
│
├── _includes/
│   ├── head.html            ← <head> contents
│   ├── header.html          ← Sticky top nav
│   ├── footer.html          ← Copyright + GitHub link
│   ├── research-breadcrumb.html   ← Breadcrumb for research pages
│   ├── publication-item.html      ← One full publication citation
│   ├── tag-filter-script.html     ← Shared filter JS (pubs + presentations)
│   ├── theme-recent-results.html  ← Auto-pulled recent papers (by tag)
│   └── theme-team.html      ← Auto-pulled team members (by tag)
│
├── _data/                   ← All repeatable content lives here
│   ├── research_themes.yml  ← Six research themes (drives home & hub)
│   ├── tag_labels.yml       ← Display labels for tags (used everywhere)
│   ├── people.yml           ← Current group members
│   ├── people_groups.yml    ← Role-grouping definitions (PI/PDRA/PhD/…)
│   ├── alumni.yml           ← Past group members
│   ├── group_photos.yml     ← Year-tabbed group photo widget data
│   ├── achievements.yml     ← Awards / grants / theses / milestones / media
│   ├── publications.yml     ← Papers (refereed, preprint, proceedings)
│   ├── presentations.yml    ← Talks (research, public, seminar, poster)
│   ├── engagement_activities.yml  ← Public-engagement activity list
│   ├── engagement_resources.yml   ← Group + external resources
│   ├── open_positions.yml   ← Advertised opportunities (Join landing)
│   ├── phd_scholarships.yml ← PhD funding routes / scholarships
│   ├── postdoc_fellowships.yml    ← Postdoctoral fellowship schemes
│   └── mphys_past_projects.yml    ← Past Masters project examples
│
├── assets/
│   └── styles.css           ← All visual design
│
├── index.html               ← Home page
├── people.html              ← People page
├── engagement.html          ← Public engagement page
├── contact.html             ← Contact page
├── 404.html                 ← Styled "page not found"
├── research/
│   ├── index.html           ← Research hub
│   ├── phenomenology.md      ← Theme page
│   ├── darkside.md           ← Theme page
│   ├── instrumentation.md    ← Theme page
│   ├── levitating.md         ← Theme page
│   ├── neutrinos.md          ← Theme page
│   ├── colliders.md          ← Theme page
│   ├── publications.html     ← Publications (tag-filtered, year breaks)
│   ├── presentations.html    ← Presentations (category-filtered)
│   └── achievements.html     ← Achievements (reverse-chrono list)
├── join/
│   ├── index.html           ← Join landing (advertised opportunities + level boxes)
│   ├── masters.html         ← Masters / undergraduate research
│   ├── phd.html             ← PhD opportunities + scholarship list
│   ├── postdoc.html         ← Postdoctoral fellowships
│   └── phd/
│       └── advice.html      ← Advice on applying for a PhD (prose)
├── README.md
└── LICENSE
```

All the planned pages are now in place. To extend the site, add a page
file with the appropriate `layout` (`default`, `subpage`, or `theme`) and,
where content repeats, a matching `_data/*.yml` file — every section above
follows that pattern.

---

## Editing content

### Add a publication

Open `_data/publications.yml`, append an entry. The home page's
"Recent" box and the publications page both pick it up automatically.
Newer dates appear first.

```yaml
- date: 2026-04-22
  title: "Your paper title here"
  authors:
    - "First Author"
    - "Second Author"
    - "Third Author"
    - "Fourth Author"           # if more than 4, layout shows
                                # "First Author et al."
  journal: "Phys. Rev. D"       # short journal name (optional for preprints)
  doi: "https://doi.org/10.1103/PhysRevD.XXX.XXXXXX"
  arxiv_id: "2604.12345"
  arxiv_cat: "hep-ex"
  inspire: "https://inspirehep.net/literature/XXXXXXX"
  type: published               # or "preprint" or "conf-proceedings"
  tags: [darkside, AI]          # see tag vocabulary below
  # --- optional explainer (adds an expandable pane with a down-arrow) ---
  explainer: >-                 # plain-language paragraph on the key result
    Short summary of the idea / result / impact.
  explainer_image: "/assets/images/publications/my-plot.png"   # one key plot
  explainer_image_caption: "Optional caption."
```

If neither `explainer` nor `explainer_image` is set, the paper shows no
expansion arrow. Drop key plots into `assets/images/publications/`.

### Add an achievement

Open `_data/achievements.yml`, append an entry. Newer dates appear
first; the top three feed the home page "Recent news" box.

```yaml
- date: 2026-05-10
  type: Award                   # Award | Grant | Thesis | Milestone | Media
  title: "Headline of the achievement"
  body: >-
    Optional longer description. Markdown is OK.
  link: "https://optional.url"
```

### Add a presentation

Open `_data/presentations.yml`, append an entry.

```yaml
- date: 2026-06-01
  title: "Talk title"
  speaker: "Speaker name"
  venue: "Conference name"
  location: "City, Country"
  slides: "https://optional.url/to/slides.pdf"
  recording: "https://optional.url/to/recording"
  tags: [research-talk, darkside]   # see tag vocabulary below
```

### Add a public-engagement activity or resource

Activities live in `_data/engagement_activities.yml` (reverse-chrono list
on `/engagement/`). A `description` is optional; when present, a "More"
toggle expands an inline description.

```yaml
- date: 2026-05-01
  title: "Activity title"
  type: "Public lecture"          # free text
  audience: "General public"
  link: "https://optional.url"
  image: ""                       # /assets/images/engagement/foo.jpg
  description: ""                 # optional; adds an expandable pane
```

Resources live in `_data/engagement_resources.yml`, split by `group`
into "From the group" (`own`) and "Elsewhere" (`external`):

```yaml
- group: own                      # own | external
  title: "Resource title"
  type: "Video"                   # Video | Article | Activity pack | ...
  description: "One-line description."
  link: "https://..."
  source: ""                      # attribution (mainly for external)
```

The speaker call-to-action text on `/engagement/` is holding text in
`engagement.html` — edit it directly.

### Manage Join opportunities

**Advertised opportunities** (the colour-coded highlights below the hero of
`/join/`) live in `_data/open_positions.yml`. The `level` field drives the
colour (masters = sage, phd = amber, postdoc = periwinkle). Empty the file
of entries and the "Advertised opportunities" section disappears.

```yaml
- level: phd                      # masters | phd | postdoc
  title: "Position title"
  summary: "One-line description."
  deadline: "Applications close …"
  link: ""                        # advert URL; empty → links to /join/<level>/
```

**PhD scholarships** are in `_data/phd_scholarships.yml`; **postdoc
fellowships** in `_data/postdoc_fellowships.yml`. Both render as structured
cards on their sub-pages. The scheme *names* are filled in; deadlines,
contact-by dates, and requirements are `EDIT ME` placeholders — check each
scheme's official page before publishing.

```yaml
# phd_scholarships.yml
- title: "Scheme name"
  eligibility: "Home & International"
  deadline: "…"
  contact_by: "…"
  formal: "Formal requirements."
  practical: "Practical advice."
  link: ""
```

**Masters past projects** are in `_data/mphys_past_projects.yml`
(`year`, `title`, optional `student`).

The prose on the Join landing and sub-pages is written in the first person
(group lead's voice) and is holding text — edit each `.html` file in `join/`
directly. The three level boxes on `/join/` are plain text cards styled like
the research themes; the quick-nav row beneath the hero jumps to them. To add
a figure to a sub-page, the `subpage` layout currently has no figure slot;
ask if you'd like one added.

### Contact details

`contact.html` holds the group's contact block — group lead, email,
LinkedIn, a **Bluesky placeholder** (`EDIT ME` — swap in the real handle),
postal address, and GitHub. Edit the file directly.

### The 404 page

`404.html` is served automatically by GitHub Pages for unknown URLs. It
reuses the site header, footer, and styling; edit its copy directly.

### Add or update a group member

Open `_data/people.yml`. Each member is a YAML entry. The page groups
entries by their `group:` field, in the order defined by
`_data/people_groups.yml`. Within each group, list members in your
intended display order — the convention is **reverse chronological by
start year**, alphabetical by surname within the same year.

```yaml
- id: jane-doe
  name: "Jane Doe"
  honorific: "Dr."                  # "Prof." | "Dr." | "" — rendered muted
  surname: "Doe"
  role: "Postdoctoral Research Associate"
  group: postdoc                    # pi | postdoc | phd | pgmasters | ugmasters
  start_year: 2024                  # integer — null for PI/postdocs if not relevant
  bio: >-
    Two-line research-focus paragraph. Leave "" to show a soft
    "Research focus to come." placeholder.
  themes: [darkside, instrumentation, mlai]   # slugs from tag_labels.yml
  experiments: []                   # forward-compat, leave empty for now
  email: "jane.doe@manchester.ac.uk"
  orcid: "https://orcid.org/0000-0000-0000-0000"
  website: ""
  linkedin: ""
  github: ""
  bluesky: ""
  photo: ""                         # /assets/images/people/jane-doe.jpg
                                    # leave "" for an initials placeholder
```

Drop a portrait into `assets/images/people/` and set `photo:` to its
path. Initials are shown automatically when `photo` is empty.

### Add or reorder a role group

Open `_data/people_groups.yml`. This file controls the **order** in
which members appear in the single continuous grid on `/people/`
(currently: PI → Postdoc → PhD → Postgraduate Masters → Undergraduate
Masters & Summer). Members are shown as one uniform grid with no
section headings.

```yaml
- key: visiting                     # used as the `group:` value in people.yml
  label: "Visiting Researchers"     # retained for future use (not rendered)
  anchor: "Visiting"                # retained for future use (not rendered)
```

Append an entry to add a new group; reorder entries to change where its
members appear in the grid. The `label` / `anchor` fields are kept in
case section headings are reintroduced later, but are not currently
displayed.

Card heights are equalised to the tallest card by a small script, so
varying bio lengths and tag counts won't make the grid ragged.

### Add an alumni entry

Open `_data/alumni.yml`. Entries are sorted alphabetically by surname
at build time. The schema includes a research-focus bio and theme
tags so alumni cards carry the same context as current members.

```yaml
- id: jane-doe
  name: "Jane Doe"
  honorific: "Dr."
  surname: "Doe"
  role_while_here: "PhD student"
  dates: "2018–2022"                  # en-dash, not hyphen
  bio: >-
    Research focus while in the group — 1–2 sentences. Leave "" to omit.
  themes: [darkside, phenomenology]   # slugs from tag_labels.yml
  current_position: "Senior Physicist, CERN"
  current_position_link: "https://home.cern/"
```

### Update the group photo

Open `_data/group_photos.yml`. Add an entry per year — the page sorts
in reverse chronological order and shows year tabs above the photo so
visitors can flip between past years.

```yaml
- year: 2026
  image: "/assets/images/group/2026.jpg"   # leave "" for placeholder
  caption: "Optional caption."
```



### Edit a research theme page

Each theme is a Markdown file in `research/` (e.g. `research/darkside.md`)
using the `theme` layout. The prose (Overview, Current activities,
Collaborations) is plain Markdown in the body — edit it directly. Two
sections are generated automatically and should **not** be hand-edited:

- **Recent results** — the four most recent publications whose `tags`
  include this theme's tag, from `_data/publications.yml`.
- **Team on this theme** — members whose `themes` include this theme's
  tag, from `_data/people.yml`.

To add a figure, drop an image in `assets/images/` and set `image:` in
the page front matter; otherwise a "Figure to come" placeholder shows.

> The theme prose currently shipped is **holding text** (best-guess) —
> review and replace each section with the group's own wording.

### Add or reorder a research theme

Open `_data/research_themes.yml`. Theme order on the home page and the
research hub mirrors the order of entries in this file. A new theme also
needs a page file at `research/<slug>.md` and a tag in
`_data/tag_labels.yml`.

### Tag vocabulary

Free tags (publications + presentations), expandable but try to reuse:

| Tag              | Display label       | Maps to research theme                |
|------------------|---------------------|---------------------------------------|
| `darkside`       | DarkSide            | DarkSide experiment                   |
| `phenomenology`  | Phenomenology       | Direct dark matter phenomenology      |
| `instrumentation`| Instrumentation     | Instrumentation development           |
| `quantumsensors` | Levitating sensors  | Opto-mechanical levitating sensors    |
| `neutrinos`      | Neutrinos           | Neutrinos                             |
| `colliderphysics`| Collider physics    | Collider physics                      |
| `mlai`           | ML/AI               | (theme-agnostic; cross-cutting)       |

Display labels are configured in `_data/tag_labels.yml`. Add a new
slug → label there before using it on a paper or person.

Category tags for **publications**: `published`, `preprint`,
`conf-proceedings` (set via `type:` field).

Category tags for **presentations**: `research-talk`, `public-lecture`,
`seminar`, `poster`.

---

## Editing styles

All visual design is in `assets/styles.css`. The most impactful
parameters are the CSS variables at the top of the file: colours, fonts,
spacing, container widths. Retheme the site by changing a handful of
variables.

---

## Local preview

```bash
# One-time setup (requires Ruby 3.x):
gem install bundler
bundle install

# Run a local server with live reload:
bundle exec jekyll serve --livereload

# Then open http://127.0.0.1:4000
```

If you'd rather skip Ruby entirely, you can preview without Jekyll by
opening `index.html` in a browser, but the data-driven sections (theme
cards, recent boxes) will be empty because Liquid templates won't be
processed.

---

## Deployment

GitHub Pages is configured automatically for repositories named
`<org>.github.io`. To verify or change settings:

1. Go to the repository on GitHub.
2. **Settings → Pages**.
3. Source: `Deploy from a branch`, branch `main`, folder `/ (root)`.

Pushes to `main` rebuild and deploy the site within a minute or two.

For a custom domain (e.g. `darkmatter.manchester.ac.uk`), add a `CNAME`
file containing the domain and configure DNS records as instructed by
GitHub.

---

## License

Site content (text, images authored by group members) is © Dark Matter
Manchester, University of Manchester. The site template (HTML, CSS,
Jekyll structure) is released under the MIT License — see `LICENSE`.
