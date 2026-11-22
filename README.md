# depquiet-npm-fixpr-test

A small npm project, vulnerable on purpose, to show [depquiet](https://github.com/samuelrojas-dev/depquiet)'s
npm fix plan in a real pull request. **Do not use it for anything.**

What is in it:

- `express` 4.19.2, pinned exactly: its own advisories, and those of body-parser, cookie,
  path-to-regexp, qs, send and serve-static, close with express 4.22.3.
- `glob` 7.2.0 with `minimatch` 3.0.4 in the lock: fixed by `npm update`, within range.
- `@tailwindcss/typography` 0.5.19, which pins `postcss-selector-parser` to exactly 6.0.10.
  npm audit's fix for it is `@tailwindcss/typography` 0.5.4, a downgrade. depquiet instead
  adds an `overrides` entry scoped to typography, with postcss-selector-parser 6.1.5.

The workflow in `.github/workflows/depquiet.yml` runs the depquiet Action with
`fix-pr: true`, which opens one pull request with the verified change.
