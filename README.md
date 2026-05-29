# hugo-techly

Example site and live showcase for **[Techly](https://github.com/m1rm/techly)** — a minimal Hugo theme for tech blogs.

**Live demo:** [m1rm.github.io/hugo-techly](https://m1rm.github.io/hugo-techly/)

The theme itself lives in a separate repository. This project holds the sample content, site configuration, and GitHub Pages deployment — use it as a reference when building your own site with Techly.

> **Note:** Techly is under active development. Pin a theme version in production if you need stable builds (currently **v2.0.1**).

## Quick start

Prerequisites: [Hugo Extended](https://gohugo.io/installation/) and Go.

```bash
git clone https://github.com/m1rm/hugo-techly.git
cd hugo-techly

hugo mod get
hugo server -D
```

Open the URL Hugo prints (this site uses a GitHub Pages subpath, so local preview is typically `http://localhost:1313/hugo-techly/`).

## Using Techly in your own site

Add the theme as a Hugo module in your `hugo.toml`:

```toml
[module]
  [[module.imports]]
    path = 'github.com/m1rm/techly/v2'
    version = 'v2.0.1'
```

Then fetch dependencies and build:

```bash
hugo mod get
hugo server -D
```

See the [Getting Started](https://m1rm.github.io/hugo-techly/posts/getting-started-with-techly/) post on the demo site for configuration examples.

## Repository layout

| Path | Purpose |
|------|---------|
| `content/` | Example pages and posts |
| `hugo.toml` | Site configuration and menus |
| `static/` | Static assets (e.g. favicon) |
| `go.mod` / `go.sum` | Pinned theme module version |
| `.github/workflows/` | GitHub Pages deployment |

## Deployment

Pushes to `main` build the site with Hugo and deploy to GitHub Pages via GitHub Actions. No extra steps are required once Pages is enabled for the repository.

## Links

- **Theme:** [github.com/m1rm/techly](https://github.com/m1rm/techly)
- **Showcase (this repo):** [github.com/m1rm/hugo-techly](https://github.com/m1rm/hugo-techly)
- **Author:** [Miriam Müller](https://miriam-mueller.com)

## License

This example site is published under the same license as the repository root. The Techly theme is licensed separately — see the [theme repository](https://github.com/m1rm/techly).
