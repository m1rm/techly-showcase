+++
title = 'Getting Started with Techly'
date = 2023-01-15T09:00:00-07:00
draft = false
description = 'Install Techly as a Hugo module and start building a clean, accessible tech blog in minutes.'
tags = ['hugo', 'theme']
toc = true
+++

Techly is installed as a Hugo module. Add it to your site's configuration:

```toml
[module]
  [[module.imports]]
    path = 'github.com/m1rm/techly'
    version = 'v0.2.0'
```

Then run `hugo mod get` and start the development server with `hugo server -D`.

## What you get

The theme provides a home page that lists your recent posts, section pages for archives, and single-page layouts for individual articles.

## Configuration

Set your site title, subtitle, and author in `hugo.toml`:

```toml
[params]
  subtitle = 'Technical articles and notes'
  [params.author]
    name = 'Your Name'
```
