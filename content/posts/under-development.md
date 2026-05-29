+++
title = 'Techly is under active development'
date = 2026-05-08T09:00:00+02:00
year = '2026'
draft = false
description = 'Techly is a work in progress. This showcase site tracks the theme as it evolves — expect changes, rough edges, and occasional breaking updates.'
tags = ['general']
toc = true
pinned = true
pinnedIndicator = true
+++

If you landed here looking for a polished, finished Hugo theme — welcome anyway, but fair warning first: **Techly is under active development**.

**Techly 2.0** is out ([v2.0.1](https://github.com/m1rm/techly/releases/tag/v2.0.1) is the first installable v2 module release). This site runs that line of the theme. Layouts and configuration are more stable than in early v0.x days, but the project is still evolving.

This site is the live example for the theme. What you see today is real and usable, but it is not a frozen product. Layouts, configuration options, and styling can still change between releases.

## What that means for you

**Pin a version.** Add `version = 'v2.0.1'` (or newer) under your module import in `hugo.toml` and run `hugo mod get` when you want predictable builds.

**This site follows the theme.** [hugo-techly](https://github.com/m1rm/hugo-techly) exists to demonstrate Techly on GitHub Pages. When the theme updates, this example site updates with it — consider it a preview, not a promise of stability.

**Feedback is welcome.** Bug reports, layout ideas, and pull requests on the [theme repository](https://github.com/m1rm/techly) help shape what Techly becomes.

## What works today

Techly already covers the basics of a small tech blog:

- Home page with featured post, grid, and pagination
- Single-post layouts with optional table of contents and related articles
- Archive and search pages
- Post series with series index, term pages, and in-article navigation
- Client-side search with inline suggestions in the header
- Dark mode, syntax highlighting, and responsive navigation
- Footer social links and optional `assets/css/custom.css` overrides
- Hugo module installation — no git submodules required

Sample posts on this site show tags, page bundles with images, and typical front matter. They are here to exercise the theme, not to teach Hugo from scratch.

## What is still evolving

I am building Techly for my own blog first: simple, opinionated, and free of integrations I do not need. That means some areas are intentionally minimal, and others are not done yet.

Planned or in-progress work includes refinements to typography and documentation. Major versions may still include breaking changes — check release notes before upgrading.

## How to follow along

- **Theme source:** [github.com/m1rm/techly](https://github.com/m1rm/techly)
- **This showcase:** [github.com/m1rm/hugo-techly](https://github.com/m1rm/hugo-techly) — deployed at [m1rm.github.io/hugo-techly](https://m1rm.github.io/hugo-techly/)
- **Releases:** watch the theme repo for tagged versions when you want to upgrade deliberately

Start with the [Configuration overview]({{< relref "configuration-overview" >}}) and [Getting Started]({{< relref "getting-started-with-techly" >}}) posts in the **Using Techly** series. If you are experimenting locally, see [Developing Techly locally]({{< relref "developing-locally" >}}).
