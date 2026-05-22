+++
title = 'Images in Posts'
date = 2023-03-15T11:00:00-07:00
draft = false
tags = ['hugo', 'content']
+++

Page bundles are a convenient way to keep images alongside the content that
references them. Place media files in the same directory as the post's `index.md`:

```text
content/posts/my-post/
├── index.md
└── screenshot.png
```

Reference the image in Markdown with a relative path:

![Bryce Canyon National Park](bryce-canyon.jpg)

Hugo resolves bundle resources automatically, so images stay organized and
portable as your site grows.
