# danmenjivar.com

Personal website and blog for [Daniel Menjivar](https://danmenjivar.com), built with [Hugo](https://gohugo.io) and the [hugo-coder](https://github.com/luizdepra/hugo-coder) theme.

## Requirements

- Hugo v0.161.1+ (extended)

## Local Development

```bash
hugo serve
```

## Build

```bash
hugo build
```

Output goes to `public/`.

## Deployment

Deployed automatically via [Netlify](https://netlify.com) on push to `master`. Set the `HUGO_VERSION` environment variable in Netlify to match the version above.

## Structure

```
content/
  posts/       # Blog posts
  portfolio/   # Portfolio page
  about/       # About page
static/
  uploads/     # Images and resume PDF
assets/
  css/         # Custom styles (custom.css)
layouts/
  _partials/   # Theme overrides
  shortcodes/  # Custom shortcodes (portfolioEntry, buttonShort)
themes/
  hugo-coder/  # Git submodule
```

## Theme

hugo-coder is included as a git submodule. After cloning:

```bash
git submodule update --init
```
