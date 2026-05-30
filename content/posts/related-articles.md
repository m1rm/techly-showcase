+++
title = 'Related Articles'
date = 2026-05-19T09:00:00+02:00
year = '2026'
draft = false
description = 'How Techly picks related posts at the end of an article, and how to tune the section with params.related.'
tags = ['feature']
series = ['Using Techly']
toc = true
index = true
+++

At the bottom of every blog post, Techly can show a **related articles** grid: cover image, title, excerpt, and date. Under that, an optional button links readers to a tag archive — for example “More in hugo”.

The feature is on by default. You control it entirely from site configuration; no shortcodes required.

## Where it appears

Related posts render on **single post pages** in your main content section (by default `posts`). Standalone pages such as About or Contact do not include the block.

Techly only shows the section when Hugo finds at least one related page. If nothing matches, the whole block is omitted — no empty heading.

## How posts are chosen

Techly uses [Hugo’s built-in related content](https://gohugo.io/content-management/related/): it scores pages by shared metadata (especially **tags**) and limits the result to pages in `params.mainSections`.

Practical tips:

- **Tag your posts.** Articles with overlapping tags are more likely to surface each other. On this site, `general` and `feature` group the documentation so related cards stay on-topic.
- **Keep `mainSections` accurate.** If your blog lives in `blog/` instead of `posts/`, update `params.mainSections` so related content and the home page use the same sections.

```toml
[params]
  mainSections = ['posts']
```

## Configuration

All options live under `[params.related]` in `hugo.toml`:

```toml
[params.related]
  enabled = true
  limit = 3
  heading = 'More articles'
  moreLink = 'best'
  moreLabel = 'More in %s'
```

| Parameter | Default | Description |
| --- | --- | --- |
| `enabled` | `true` | Set to `false` to hide related posts site-wide |
| `limit` | `3` | Maximum cards in the grid |
| `heading` | `"More articles"` | Section `<h2>` text |
| `moreLink` | `"best"` | Tag button strategy (see below) |
| `moreLabel` | `"More in %s"` | Button label; `%s` is the tag name |

Theme defaults are merged from the module. Override only what you need.

### Disable related posts

```toml
[params.related]
  enabled = false
```

### Change the heading or count

```toml
[params.related]
  limit = 4
  heading = 'You might also like'
```

## The “More in …” button

Below the grid, Techly can show one or more buttons that link to **tag term pages** (`/tags/<slug>/`). This helps readers browse a whole topic, not just the few related cards above.

Set the strategy with `moreLink`:

| Value | Behavior |
| --- | --- |
| `best` | Pick the tag on this post that appears most often among the related results (default) |
| `first` | Use the first tag in the post’s front matter |
| `all` | One button per tag on the post |
| `none` | Hide the buttons |

Posts **without tags** never show a button, regardless of strategy.

Example with a custom label:

```toml
[params.related]
  moreLink = 'first'
  moreLabel = 'Browse all posts tagged %s'
```

With `moreLink = 'all'` and `tags = ['hugo', 'theme']`, readers see two buttons when both tag pages exist.

## What each card shows

Each related card uses the same cover logic as listing pages (`featuredImage`, bundle `featured.*`, or no image). The excerpt comes from `description` in front matter, or a truncated summary if description is empty.

To improve cards on posts that often appear as related content, set a clear `description` and an optional cover image — see [Featured images]({{< relref "featured-images" >}}).

## Try it on this site

Open any post in the **Using Techly** series that shares tags with others (for example this one, tagged `feature`). Scroll past the article body to see the grid and the tag archive button.
