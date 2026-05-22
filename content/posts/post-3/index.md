+++
title = 'Images in Posts'
date = 2023-03-15T11:00:00-07:00
draft = false
description = 'Keep images alongside your content with Hugo page bundles — organized, portable, and easy to reference.'
tags = ['hugo', 'content']
toc = true
+++

Page bundles are a convenient way to keep images alongside the content that references them. Place media files in the same directory as the post's `index.md`:

```text
content/posts/my-post/
├── index.md
└── screenshot.png
```

## Referencing images

Reference the image in Markdown with a relative path:

![Selfie of a woman with buzz cut black hair and sunglasses on a high wooden walkway in a forest](avatar.jpg)

Hugo resolves bundle resources automatically, so images stay organized and portable as your site grows.

## Featured images (optional)

Listing cards only show a cover when you explicitly provide one — inline content images are not used automatically.

```yaml
featured_image = 'featured.jpg'   # path or bundle filename
showImage = false                 # hide cover for this post
```

Or add a `featured.jpg` (or `featured.png`, etc.) to the page bundle.

Sit excepteur do velit veniam mollit in nostrud laboris incididunt ea.
