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
