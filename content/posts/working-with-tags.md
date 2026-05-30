+++
title = 'Working with Tags'
date = 2026-05-14T09:00:00+02:00
year = '2026'
draft = false
description = 'Use Hugo taxonomies out of the box — tag archive pages help readers discover related content.'
tags = ['general']
series = ['Using Techly']
toc = true
index = true
+++

Hugo's built-in taxonomy support works out of the box with Techly. Add tags to any post's front matter:

```toml
tags = ['general', 'feature']
```

## Tag archive pages

Each tag gets its own archive page listing all matching posts. This makes it easy for readers to discover related content across your blog.

On this showcase, documentation posts use **`general`** for setup and structure topics and **`feature`** for optional theme behavior. Shared tags also feed Techly's [related articles]({{< relref "related-articles" >}}) box at the bottom of each post.

## Best practices

Keep tag names short and consistent. A handful of well-chosen tags beats a long list of one-off labels. Reuse the same labels across posts in a series so related content and tag archives stay useful.
