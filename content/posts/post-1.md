+++
title = 'Getting Started with Techly'
date = 2023-01-15T09:00:00-07:00
draft = false
tags = ['hugo', 'theme']
+++

Techly is installed as a Hugo module. Add it to your site's configuration:

```toml
[module]
  [[module.imports]]
    path = 'github.com/m1rm/techly'
```

Then run `hugo mod get` and start the development server with `hugo server -D`.

The theme provides a home page that lists your recent posts, section pages for
archives, and single-page layouts for individual articles.
