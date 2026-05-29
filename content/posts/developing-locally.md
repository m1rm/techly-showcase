+++
title = 'Developing Techly locally'
date = 2026-05-13T09:00:00+02:00
year = '2026'
draft = false
description = 'How this example site uses a Go module replace to load the Techly theme from a sibling checkout — and what to do when Hugo serves an old copy instead.'
tags = ['general']
series = ['Using Techly']
toc = true
+++

This site ([hugo-techly](https://github.com/m1rm/hugo-techly)) is the working example for the [Techly](https://github.com/m1rm/techly) theme. In production it imports the theme as a Hugo module from GitHub. For day-to-day theme work, it loads the theme from a **local checkout** next to the site.

## Directory layout

Clone both repositories as siblings:

```text
projects/
├── techly/        ← theme source (layouts, assets, …)
└── hugo-techly/   ← this example site (content, config)
```

Hugo resolves the theme relative to the site, not from a published release, while you are developing.

## How the override works

The site still declares the module import in `hugo.toml` the usual way:

```toml
[module]
  [[module.imports]]
    path = 'github.com/m1rm/techly/v2'
    version = 'v2.0.1'
```

The local override lives in `go.mod`:

```go
module github.com/m1rm/hugo-techly

go 1.26.3

replace github.com/m1rm/techly/v2 => ../techly

require github.com/m1rm/techly/v2 v2.0.1
```

`replace` tells Go (and Hugo's module loader) to use `../techly` instead of downloading the module from the proxy. Edit files in the theme repo, save, refresh the browser — no publish step required.

You can confirm which directory Hugo uses:

```bash
hugo config mounts | rg '"dir"'
```

You should see `"dir": "/…/techly/"` pointing at your local checkout, not a path under `$GOCACHE` or `/tmp`.

## Daily workflow

```bash
cd hugo-techly
hugo server -D
```

Open `http://localhost:1313` (or the URL Hugo prints). Changes to layouts, CSS, or JS in `../techly` appear after a refresh. Hugo rebuilds assets automatically in server mode.

When you change module dependencies or suspect a stale cache:

```bash
hugo mod clean --all
hugo server -D
```

## Common gotchas

### Stale `_vendor/` directory

If you ever ran `hugo mod vendor`, Hugo may prefer the copied theme in `_vendor/` over your local checkout. That directory is easy to miss — you edit `../techly`, but the site still serves an old vendored copy.

Remove it and rebuild:

```bash
rm -rf _vendor
hugo mod clean --all
hugo server -D
```

This repo gitignores `_vendor/` so it does not come back from a commit by accident.

### Module cache

Hugo caches downloaded modules. After changing `go.mod` or the replace path, run `hugo mod clean --all` once so the loader picks up the local theme.

### `go.work` vs `replace`

A Go workspace file (`go work init . ../techly`) can work, but it is easy to combine with `_vendor/` or a warm module cache and still see old templates. A single **`replace` in `go.mod`** is the setup used here — explicit and easy to inspect.

GitHub Actions cannot rely on a sibling folder that only exists on your machine. The deploy workflow checks out **both** repositories:

```yaml
- name: Checkout site
  uses: actions/checkout@v4
  with:
    path: hugo-techly

- name: Checkout theme
  uses: actions/checkout@v4
  with:
    repository: m1rm/techly
    path: techly

- name: Build site
  working-directory: hugo-techly
  run: hugo mod get && hugo --minify
```

On the runner the layout matches local development:

```text
workspace/
├── hugo-techly/
└── techly/
```

The same `replace github.com/m1rm/techly/v2 => ../techly` in `go.mod` resolves correctly in CI when both repos are present. Production builds without `replace` download **v2.0.1** from the module proxy.

## Using a published theme again

To build against a tagged release from GitHub instead of the local checkout:

1. Remove or comment out the `replace` line in `go.mod`
2. Run `hugo mod get github.com/m1rm/techly/v2@v2.0.1` (or the version you need)
3. Run `hugo mod clean --all` and rebuild

## Summary

| Context | Theme source |
|---------|----------------|
| Local dev | `../techly` via `go.mod` replace |
| Downstream sites | `github.com/m1rm/techly/v2` from the module proxy, no replace |

Keep the two repos side by side, avoid `_vendor/` during theme work, and clear the module cache when something looks outdated. That is all you need for a fast local theme loop.

For installing Techly in a new site without local development, see [Getting Started with Techly]({{< relref "getting-started-with-techly" >}}).
