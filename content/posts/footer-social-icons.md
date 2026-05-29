+++
title = 'Footer Social Icons'
date = 2026-05-20T09:00:00+02:00
year = '2026'
draft = false
description = 'Add GitHub, Mastodon, or other links to the footer with menus.social and SVG icons in assets/icons/.'
tags = ['feature']
series = ['Using Techly']
toc = true
+++

Techly can show a row of **social links** in the site footer — icon buttons with accessible text, opening external profiles in a new tab when the URL is absolute.

Nothing is hard-coded. You define links in `hugo.toml` and supply matching SVG files in your site’s `assets/` tree.

## Enable or disable the block

Footer social links are controlled by a theme parameter and a Hugo menu.

```toml
[params.footer]
  showSocial = true
```

Set `showSocial = false` to hide the icon row entirely, even if a `social` menu exists.

If the menu is empty, Techly renders nothing — no placeholder icons.

## Step 1: Add SVG icons

Place one SVG per network in **`assets/icons/`** at the root of your site (not inside the theme module):

```text
assets/icons/
├── github.svg
├── mastodon.svg
└── rss.svg
```

Techly loads them with `resources.Get` and inlines the markup into the footer. Use simple, single-color SVGs; they inherit footer link colors and hover styles.

The file name (without `.svg`) is what you reference in menu params — for `github.svg`, use `icon = 'github'`.

## Step 2: Define the social menu

Add entries under `menus.social` in `hugo.toml`:

```toml
[[menus.social]]
  name = 'GitHub'
  url = 'https://github.com/m1rm/techly'
  weight = 10
  [menus.social.params]
    icon = 'github'

[[menus.social]]
  name = 'RSS'
  url = '/index.xml'
  weight = 20
  [menus.social.params]
    icon = 'rss'
```

| Field | Purpose |
| --- | --- |
| `name` | Accessible label (shown in a visually hidden span) |
| `url` | Link target — `http`/`https` links open in a new tab with `rel="noopener noreferrer"` |
| `weight` | Sort order (lower first) |
| `params.icon` | Base name of `assets/icons/<icon>.svg` |

Optional `params.rel` on a menu entry is passed through for non-HTTP URLs (for example `rel = 'alternate'` on a feed link).

## How it looks in the markup

The footer partial wraps links in a `<nav aria-label="Social links">` list. Each item is an anchor with:

- an inline SVG inside `.footer-social-icon` (decorative, `aria-hidden="true"`)
- a `.visually-hidden` span with the menu `name` for screen readers

External links do not rely on icon shape alone for meaning — always set a clear `name`.

## Full example

Minimal site footer with social links and copyright:

```toml
[params.footer]
  since = 2020
  tagline = 'Built with Hugo and Techly.'
  copyright = 'Your Name'
  showSocial = true

[[menus.social]]
  name = 'GitHub'
  url = 'https://github.com/your-user'
  weight = 10
  [menus.social.params]
    icon = 'github'
```

Pair this with `assets/icons/github.svg`. Run `hugo server` and check the footer on any page.

## Troubleshooting

**Icons missing but links appear.** The `icon` param does not match any file under `assets/icons/`, or the SVG path is wrong. Confirm the file exists and Hugo sees your site `assets/` directory.

**Nothing in the footer.** Check `showSocial`, confirm `[[menus.social]]` entries exist, and verify `icon` names match your files.

**Theme module vs site assets.** Icons must live in **your** site repository. The theme does not ship network logos — you choose which networks to support and which artwork to use.
