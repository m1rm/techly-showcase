+++
title = 'Controlling Search Indexing'
date = 2026-05-21T09:00:00+02:00
year = '2026'
draft = false
description = 'Use front matter and theme parameters to control robots meta tags and sitemap.xml with Techly’s opt-in indexing model.'
tags = ['feature']
series = ['Using Techly']
toc = true
index = true
+++

Techly ships with an **opt-in indexing model**. By default, pages are **not** indexed and are **excluded** from `sitemap.xml`. You decide explicitly which content search engines should discover.

This post covers the front matter and `hugo.toml` settings involved. For background on robots meta tags and sitemaps in general, see the [SEO Basics: Indexing](https://miriam-mueller.com/series/seo-basics-indexing/) series on my blog.

## TL;DR

- Set `index = true` in post or page front matter for content that should be indexed.
- Techly outputs `<meta name="robots" content="index">` or `noindex` accordingly.
- `sitemap.xml` lists only pages with `index = true`, plus the home page when `params.indexHome` is enabled (default).
- Override per page with `robots = "noindex, follow"` when you need finer control.
- Point crawlers at your sitemap in `static/robots.txt`.

## Opt-in by default

Most Hugo themes include every generated page in `sitemap.xml` and leave robots meta tags unset. That often means tag archives, search pages, and section listings end up in search indexes alongside your articles.

Techly inverts that default:

| Page type | Without `index = true` | With `index = true` |
| --- | --- | --- |
| Posts and pages | `noindex`, omitted from sitemap | `index`, listed in sitemap |
| Tag / series / search pages | `noindex`, omitted | Only if you set `index = true` |
| Home page | Indexed when `indexHome = true` (default) | Same |

> **Note:** Because indexing is opt-in, **remember `index = true` on every post you want in search results**. Auto-generated listing pages stay excluded unless you explicitly opt them in.

## Front matter: `index`

Add to any post or page:

```toml
index = true
```

Example for a published article:

```toml
+++
title = 'My Article'
date = 2026-05-21T09:00:00+02:00
description = 'A short summary for cards and meta tags.'
tags = ['hugo']
index = true
+++
```

Techly’s `layouts/_partials/head.html` turns that into:

```html
<meta name="robots" content="index">
```

Pages without `index = true` (or with `index = false`) get:

```html
<meta name="robots" content="noindex">
```

## Home page: `params.indexHome`

The home page is treated separately. It is indexed and included in `sitemap.xml` by default, even without front matter on `content/_index.md`.

Disable that in your site’s `hugo.toml`:

```toml
[params]
  indexHome = false
```

When `indexHome` is `true` (the theme default), the home page gets `content="index"` and appears in the sitemap alongside opted-in posts.

## Override with `robots`

For cases like `noindex, follow`, set a custom value. It overrides the `index` setting:

```toml
robots = 'noindex, follow'
```

Use this when a page should stay out of the index but you still want crawlers to follow its links.

## Sitemap.xml

Techly provides `layouts/_default/sitemap.xml`. It lists:

- pages with `index = true`
- the home page when `params.indexHome` is enabled

You do not need a site-level override unless you want different rules.

After building, check `public/sitemap.xml`. It should contain your opted-in posts (and the home URL), not tag or search pages.

## robots.txt

A sitemap helps discovery; it does not control indexing. Keep excluded pages out of the sitemap and use robots meta tags as described above.

Add or extend `static/robots.txt`:

```text
User-agent: *
Allow: /

Sitemap: https://example.com/sitemap.xml
```

Replace the URL with your production `baseURL`.

## Checklist for a new site

1. Add `index = true` to each post and page you want indexed.
2. Leave `indexHome = true` (default) if the home page should appear in search.
3. Verify `public/sitemap.xml` after `hugo build`.
4. Add a `Sitemap:` line to `static/robots.txt`.
5. Submit the sitemap in Google Search Console or your search tool of choice.

## Related configuration

Site-wide parameters and other front matter keys are summarized in [Configuration overview]({{< relref "configuration-overview" >}}). Content paths and `static/robots.txt` are covered in [Content folder structure]({{< relref "content-folder-structure" >}}).
