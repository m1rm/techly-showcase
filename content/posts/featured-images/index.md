+++
title = 'Featured Images'
date = 2026-05-17T09:00:00+02:00
year = '2026'
draft = false
description = 'Add a cover image to listing cards with featuredImage or a featured.* bundle resource.'
tags = ['feature']
series = ['Using Techly']
toc = true
index = true
featuredImage = 'featuredImageShowcase.jpg'
imageAlt = 'Techly blog listing card with a featured cover image'
+++

Listing cards can show a cover image when you opt in — inline images in the article body are not used automatically.

## Set a featured image

Add `featuredImage` to front matter with a path or bundle filename:

```toml
featuredImage = 'featuredImageShowcase.jpg'
imageAlt = 'Description for screen readers and when the image fails to load'
```

This post uses a page bundle:

```text
content/posts/featured-image/
├── index.md
└── featuredImageShowcase.jpg
```

## Alternative: featured.* in the bundle

If the file is named `featured.jpg`, `featured.png`, or similar, Techly picks it up without front matter:

```text
content/posts/my-post/
├── index.md
└── featured.jpg
```

## Hide the cover for one post

```toml
showImage = false
```

Check the home page and `/posts/` — this article should appear with the cover above the title on its card.

![Featured image showcase in a listing card](featuredImageShowcase.jpg)
