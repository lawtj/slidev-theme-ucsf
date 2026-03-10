# slidev-theme-ucsf

[![NPM version](https://img.shields.io/npm/v/slidev-theme-ucsf?color=3AB9D4&label=)](https://www.npmjs.com/package/slidev-theme-ucsf)

A UCSF-inspired theme for [Slidev](https://github.com/slidevjs/slidev).

<!--
  Learn more about how to write a theme:
  https://sli.dev/guide/write-theme.html
--->

<!--
  run `npm run dev` to check out the slides for more details of how to start writing a theme
-->

<!--
  Put some screenshots here to demonstrate your theme

  Live demo: [...]
-->

## Install

Add the following frontmatter to your `slides.md`. Start Slidev then it will prompt you to install the theme automatically.

<pre><code>---
theme: <b>ucsf</b>
---</code></pre>

Learn more about [how to use a theme](https://sli.dev/guide/theme-addon#use-theme).

## Layouts

This theme provides the following layouts:

- `SectionEditor`
- `TwoColumnCards`
- `ThreeColumnCards`
- `threenocard`

## Components

This theme provides the following components:

- None yet (theme-focused layouts and styles)

## Asset Pattern

For GitHub Pages deployments, keep any image that is referenced from:

- slide frontmatter like `image:` or `background:`
- Vue component props like `<RevealImage src="..." />`
- custom theme layouts/components

in `public/assets/`, and reference it with an absolute path such as `/assets/title.jpg`.

Why this pattern:

- Slidev/Vite can statically bundle images used directly in markdown like `![x](./image.png)`.
- Frontmatter values and component prop strings are not statically analyzable, so files under `assets/` can 404 after build.
- Files in `public/` are copied as-is, and the theme layouts in this repo prefix them with `import.meta.env.BASE_URL`, so they work on GitHub Pages.

Recommended examples:

```md
---
layout: image-right
image: /assets/etco2.jpg
---

<img src="/assets/cboutcomes.png" alt="Outcomes chart">

<RevealImage src="/assets/backboard.png" />
```

If you build for GitHub Pages, use a base-aware build command such as:

```bash
npm run build -- --base /<repository-name>/
```

## Publish to npm

1. Log in to npm:
   ```bash
   npm login
   ```
2. Verify what will be published:
   ```bash
   npm run pack:check
   ```
3. Publish:
   ```bash
   npm publish --access public --cache .npm-cache
   ```

If you are doing a new release, bump first:

```bash
npm version patch
```

## Contributing

- `npm install`
- `npm run dev` to start theme preview of `example.md`
- Edit the `example.md` and style to see the changes
- `npm run export` to generate the preview PDF
- `npm run screenshot` to generate the preview PNG
