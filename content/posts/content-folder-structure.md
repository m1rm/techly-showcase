+++
title = 'Content Folder Structure'
date = 2026-05-12T09:00:00+02:00
year = '2026'
draft = false
description = 'Where to put posts, series, search, and static pages so Techly layouts and menus work as intended.'
tags = ['general']
series = ['Using Techly']
toc = true
+++

Techly does not impose a proprietary content format — it is a standard Hugo site with opinionated **paths and layouts**. If files live in the expected places, menus, search, series, and listing pages work without extra configuration.

This post describes the layout used by [this showcase](https://github.com/m1rm/hugo-techly) and what you can adapt. Site-wide settings are covered in [Configuration overview]({{< relref "configuration-overview" >}}).

## Overview

```text
content/
├── _index.md              # Home page body (optional intro text)
├── about.md               # Regular page
├── contact.md
├── archive.md             # layout: archive
├── search.md              # layout: search
├── posts/
│   ├── _index.md          # Section title for /posts/
│   ├── my-post.md         # Single-file post
│   └── my-bundle/         # Page bundle post
│       ├── index.md
│       └── featured.jpg
└── series/
    ├── _index.md          # Taxonomy list at /series/
    └── using-techly/
        └── _index.md      # Series description at /series/using-techly/
```

Hugo also generates **tag** pages automatically from front matter (`/tags/<slug>/`). You do not create `content/tags/` by hand.

## Home and standalone pages

| Path | Role |
| --- | --- |
| `content/_index.md` | Optional copy above the post list on the home page. The hero title comes from `params.banner`, not this file’s title. |
| `content/about.md`, `contact.md`, … | Regular pages rendered with the page layout (optional `toc = true`). |

Link these from `menus.main` with `pageRef`:

```toml
[[menus.main]]
  name = 'About'
  pageRef = '/about/'
  weight = 30
```

## Posts section (`posts/`)

Blog articles belong in a **section** that matches `params.mainSections` (default `posts`):

```toml
[params]
  mainSections = ['posts']
```

That section drives:

- the home page post list (featured first item + grid)
- `/posts/` section listing
- the archive page
- related-articles candidates
- the JSON search index

### Section index

`content/posts/_index.md` sets the title and description for `/posts/`:

```toml
+++
title = 'Posts'
description = 'All articles published on this site.'
+++
```

### Single-file posts

```bash
hugo new posts/my-article.md
```

### Page bundles

For images beside the post, use a bundle directory — see [Images in posts]({{< relref "images-in-posts" >}}) and [Featured images]({{< relref "featured-images" >}}):

```text
content/posts/my-article/
├── index.md
├── diagram.png
└── featured.jpg
```

Techly’s `posts` layout handles single posts; leaf bundles and single files both work.

## Series taxonomy

Enable the taxonomy in site config (Hugo does not merge taxonomies from the theme module):

```toml
[taxonomies]
  tag = 'tags'
  series = 'series'
```

Tag posts with one series name:

```toml
series = ['Using Techly']
```

Optional term content for a richer series landing page:

```text
content/series/using-techly/_index.md
```

Create it with:

```bash
hugo new series/using-techly/_index.md
```

See [Organizing posts into series]({{< relref "organizing-posts-into-series" >}}) for reader-facing behavior.

## Search page

Client-side search needs:

1. JSON output on the home page (for the index)
2. A dedicated search **page**

In `hugo.toml`:

```toml
[outputs]
  home = ['HTML', 'RSS', 'JSON']
```

Create `content/search.md`:

```toml
+++
title = 'Search'
layout = 'search'
description = 'Search articles on this site.'
+++
```

Techly looks for this page at `/search/` or `/page/search/` by default. Override with:

```toml
[params]
  searchPagePath = '/search'
```

The navbar search field and the full search page both use this content file.

## Archive page

Optional chronological archive (grouped by year):

```toml
+++
title = 'Archive'
layout = 'archive'
description = 'All posts, grouped by year.'
+++
```

Like search, add a `menus.main` entry if you want it in the navigation. This showcase keeps archive out of the main menu; the layout still works at `/archive/`.

## Tags

Add tags in post front matter — no extra folders:

```toml
tags = ['general']
```

Techly renders tag lists on posts and paginated term pages at `/tags/<slug>/`.

## Site assets (not under `content/`)

Some features expect files **outside** `content/`:

| Path | Used for |
| --- | --- |
| `assets/icons/*.svg` | Footer social icons ([Footer social icons]({{< relref "footer-social-icons" >}})) |
| `assets/css/custom.css` | Site-specific style overrides |
| `static/` | Favicon, `robots.txt`, files with fixed URLs |

## Minimal checklist for a new site

1. `content/posts/` with at least one post and `_index.md`
2. `content/_index.md` if you want home intro text
3. `[taxonomies]` and `[outputs]` in `hugo.toml`
4. `content/search.md` with `layout = 'search'`
5. `menus.main` pointing at Home, Posts, and any pages you create
6. Optional: `content/archive.md`, `content/series/.../_index.md`, `assets/icons/` for social links

This showcase repo is a working reference — browse `content/` alongside these posts to see each pattern in context.
