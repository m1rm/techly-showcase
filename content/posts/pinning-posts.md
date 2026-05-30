+++
title = 'Pinning Posts'
date = 2026-05-18T09:00:00+02:00
year = '2026'
draft = false
description = 'Keep important posts at the top of your listing pages with pinned = true and an optional pin indicator.'
tags = ['feature']
series = ['Using Techly']
toc = true
index = true
+++

Use pinning when an announcement or evergreen article should stay visible above newer posts — without backdating it or bumping the publish date.

## Pin a post

Add `pinned` at the top level of the post's front matter:

```toml
+++
title = 'Important announcement'
date = 2026-05-22T15:00:00+02:00
pinned = true
+++
```

Pinned posts are sorted to the top of the home page and the **Posts** section listing (`/posts/`). Among pinned posts, the usual date order still applies — newest first.

## Show the pin indicator

To display the pin icon beside the date on listing cards, add `pinnedIndicator` alongside `pinned`:

```toml
+++
title = 'Important announcement'
date = 2026-05-22T15:00:00+02:00
pinned = true
pinnedIndicator = true
+++
```

The icon uses your theme accent color. A post can be pinned without the indicator — useful when you want top placement without drawing extra attention.

## When to use it

Pinning works well for:

- Status updates or “work in progress” notices
- A getting-started guide you always want easy to find
- A post you link to often from elsewhere

Use it sparingly. If everything is pinned, nothing stands out.

## Try it here

See the [under development]({{< relref "under-development" >}}) post on the [posts listing]({{< relref "/posts" >}}) for a live example with the pin indicator.
