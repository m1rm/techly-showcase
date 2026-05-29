+++
title = 'Organizing Posts into Series'
date = 2026-05-16T09:00:00+02:00
year = '2026'
draft = false
description = 'Group related articles into a series — Techly adds notices, navigation, and archive pages automatically.'
tags = ['feature']
series = ['Using Techly']
toc = true
+++

Techly supports post series out of the box. Use it for multi-part tutorials, migration diaries, or any set of articles that read best in order.

## Enable the series taxonomy

Add the `series` taxonomy to your site's `hugo.toml`:

```toml
[taxonomies]
  tag = "tags"
  category = "categories"
  series = "series"
```

If you override taxonomies, include the defaults you still use — Hugo replaces the whole list, it does not merge entries from the theme module.

## Tag a post

Add a `series` field to the post's front matter:

```yaml
series = ['Using Techly']
```

A post can belong to one series. The name you choose becomes the series title and URL slug (`/series/using-techly/`).

## What readers see

On each post in a series, Techly shows:

- a short notice linking to the series page
- a numbered list of all articles in the series, with the current one highlighted
- previous and next links when applicable

The series index at `/series/` lists every series on your site. Each series page lists its posts in publication order.

## Optional series descriptions

Create a term page to add a title and description for a series:

```bash
hugo new series/using-techly/_index.md
```

Edit the generated file to set the series summary. That text appears on the series index and on the series page header.
