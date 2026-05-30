+++
title = 'Getting Started with Techly'
date = 2026-05-11T09:00:00+02:00
year = '2026'
draft = false
description = 'Install Techly as a Hugo module and start building a clean, accessible tech blog in minutes.'
tags = ['general']
series = ['Using Techly']
toc = true
index = true
+++

Techly is installed as a Hugo module. Add it to your site's configuration:

```toml
[module]
  [[module.imports]]
    path = 'github.com/m1rm/techly/v2'
    version = 'v2.0.1'
```

Then run `hugo mod get` and start the development server with `hugo server -D`.

For a full list of theme defaults and required site settings, see [Configuration overview]({{< relref "configuration-overview" >}}).

Use **v2.0.1** or later — the v2.0.0 tag is not installable as a Go module.

## What you get

The theme provides a home page with a featured post and a grid for the rest, section pages for archives, single-post layouts, related articles, and paginated tag and series listings.

## Configuration

Set your site title, home banner, and author in `hugo.toml`. The **navbar** uses `title`; the **home hero** uses `params.banner`:

```toml
title = 'My Blog'

[params]
  description = 'Technical articles and notes'
  mainSections = ['posts']

  [params.banner]
    heading = 'My Blog'
    subheading = 'Technical articles and notes'

  [params.author]
    name = 'Your Name'

  [params.footer]
    since = 2026
    copyright = 'Your Name'
```

Taxonomies and JSON search output are required for series and search — see the [theme README](https://github.com/m1rm/techly#site-configuration) for the full list.

## Upgrading from v1.x

Change the module path to `github.com/m1rm/techly/v2`, pin `v2.0.1`, run `hugo mod get`, and move any `params.subtitle` value into `[params.banner]`.
