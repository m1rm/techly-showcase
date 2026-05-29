+++
title = 'Configuration Overview'
date = 2026-05-10T09:00:00+02:00
year = '2026'
draft = false
description = 'A map of hugo.toml settings for Techly — what the theme ships by default, what your site must define, and where to tune each feature.'
tags = ['general']
series = ['Using Techly']
toc = true
+++

Techly is configured through your site's `hugo.toml`, Hugo menus, and content layout. The theme module contributes **defaults** for markup and several `params` keys; other settings only work when **your site** defines them, because Hugo does not merge every table from theme modules.

This post is the umbrella reference. Follow-up articles in the **Using Techly** series go deeper on individual topics — tagged `general` for structure and setup, `feature` for optional theme behavior.

## Module import

Pin the theme as a Hugo module (v2):

```toml
[module]
  [[module.imports]]
    path = 'github.com/m1rm/techly/v2'
    version = 'v2.0.1'
```

Run `hugo mod get` after changing the version. See [Getting Started with Techly]({{< relref "getting-started-with-techly" >}}) for a minimal first site.

## What your site must define

These blocks are included in the theme's `hugo.toml` for documentation, but **Hugo replaces rather than merges** them when your site defines its own copy. Add them explicitly to your site:

```toml
[taxonomies]
  tag = 'tags'
  series = 'series'

[outputs]
  home = ['HTML', 'RSS', 'JSON']
```

| Setting | Why it matters |
| --- | --- |
| `series` taxonomy | Series notices, navigation, and `/series/` archives |
| `home` JSON output | Client-side search index |
| `tag` taxonomy | Tag pages and related-content scoring |

If you customize `[taxonomies]`, list every taxonomy you still need — do not drop `series` or `tags` by accident.

## Defaults merged from the theme

Techly's module `hugo.toml` sets the following unless your site overrides them.

### Markup

```toml
[markup.tableOfContents]
  startLevel = 2
  endLevel = 3

[markup.goldmark.renderer]
  unsafe = true
```

Table of contents on posts and pages includes headings from level 2 through 3. Goldmark renders raw HTML in Markdown when `unsafe = true` (common for figures and embedded markup).

### Parameters (`[params]`)

| Parameter | Theme default | Used for |
| --- | --- | --- |
| `mainSections` | `["posts"]` | Home list, section listings, archive, search index, related posts |
| `showPinnedIndicator` | `false` | Pin icon on cards (per-post `pinnedIndicator` still required) |
| `showPostImages` | `true` | Cover images on listing and related cards |
| `footer.showSocial` | `true` | Footer `menus.social` block |
| `related.enabled` | `true` | Related articles section on posts |
| `related.limit` | `3` | Max related cards |
| `related.heading` | `"More articles"` | Section title |
| `related.moreLink` | `"best"` | Tag button strategy |
| `related.moreLabel` | `"More in %s"` | Tag button text |

No defaults are set for `banner`, `description`, `author`, `footer.tagline`, `footer.copyright`, `footer.since`, `newsletter`, or `searchPagePath` — you supply those when needed.

### Taxonomies in the theme file

The theme lists `tag`, `category`, and `series`. Your site should mirror at least `tags` and `series` as shown above. Categories are optional; add `category = "categories"` only if you use them.

## Recommended site configuration

A practical baseline beyond theme defaults:

```toml
title = 'My Blog'
locale = 'en-us'

[params]
  description = 'Short site summary for meta tags and footer fallback.'
  mainSections = ['posts']

  [params.banner]
    heading = 'My Blog'
    subheading = 'Technical articles and notes.'

  [params.author]
    name = 'Your Name'

  [params.footer]
    since = 2026
    tagline = 'Built with Hugo and Techly.'
    copyright = 'Your Name'
```

| Parameter | Default if omitted | Notes |
| --- | --- | --- |
| `banner.heading` | empty | Home hero `<h1>`; navbar uses `title` |
| `banner.subheading` | falls back to `description` | Home hero subtitle |
| `footer.copyright` | `params.author.name` | Copyright line name |
| `footer.since` | empty | Shown before the year range in the footer |

## Menus

Techly does not define `menus.main` for you. Typical entries use `pageRef`:

```toml
[[menus.main]]
  name = 'Home'
  pageRef = '/'
  weight = 10

[[menus.main]]
  name = 'Posts'
  pageRef = '/posts/'
  weight = 20
```

Footer social links use a separate `menus.social` menu and SVG icons in `assets/icons/`. See [Footer social icons]({{< relref "footer-social-icons" >}}).

## Feature-specific parameters

Override theme defaults only where you need different behavior:

```toml
[params.related]
  enabled = false

[params.footer]
  showSocial = false
```

| Feature | Key docs |
| --- | --- |
| Related articles | [Related articles]({{< relref "related-articles" >}}) |
| Footer social | [Footer social icons]({{< relref "footer-social-icons" >}}) |
| Post series | [Organizing posts into series]({{< relref "organizing-posts-into-series" >}}) |
| Pinned posts | [Pinning posts]({{< relref "pinning-posts" >}}) |
| Covers | [Featured images]({{< relref "featured-images" >}}) |
| Search page path | `params.searchPagePath` — default tries `/search` and `/page/search` |

### Newsletter CTA (no theme default)

Shown on the **home page only** when `params.newsletter` is set:

```toml
[params.newsletter]
  title = 'Stay up to date'
  text = 'Get notified when new posts are published.'
  url = 'https://example.com/subscribe'
  label = 'Subscribe'
  external = true
```

Partial defaults inside the template: `title` → `"Stay up to date"`, button `label` → `"Subscribe now"`.

## Post and page front matter

Techly does not require custom front matter beyond normal Hugo fields. Commonly used keys:

| Field | Scope | Purpose |
| --- | --- | --- |
| `description` | posts, pages | Lead text, cards, meta |
| `tags` | posts | Taxonomy and related content |
| `series` | posts | One series name per post |
| `toc` | posts, pages | In-page table of contents |
| `featuredImage` / bundle `featured.*` | posts | Listing and related covers |
| `pinned` / `pinnedIndicator` | posts | Sort order and pin icon |
| `layout` | pages | `search`, `archive` for special pages |

Per-post `params.showImage = false` hides the cover for that article. Site-wide `params.showPostImages = false` disables covers everywhere.

## Content layout expectations

Techly expects a `posts` section (or whatever you set in `mainSections`), optional `content/search.md` with `layout = 'search'`, and optional series term pages under `content/series/`. See [Content folder structure]({{< relref "content-folder-structure" >}}).

## This showcase site

[hugo-techly](https://github.com/m1rm/hugo-techly) extends the defaults with banner text, author, footer, newsletter CTA, and taxonomies. Compare its [`hugo.toml`](https://github.com/m1rm/hugo-techly/blob/main/hugo.toml) with the [theme defaults](https://github.com/m1rm/techly/blob/main/hugo.toml) when in doubt about what comes from the module versus your own site.

## Reading order

Posts in **Using Techly** are dated from general to specific:

1. **general** — configuration, install, folders, tags, media
2. **feature** — series, covers, pinning, related posts, social footer

Shared tags within each group help the related-articles box suggest the next doc to read.
