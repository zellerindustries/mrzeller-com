# Hans Zeller personal site

Minimal static Italian site (`lang="it"`) built with `@minimaz/sitekit`: an "In arrivo" index and a link-in-bio page. No JS, no forms, no `src/scripts/`.

## Commands

```bash
npm run build          # mz b --overwrite
npm start              # build, then serve ./dist
npm run format         # prettier --write .
npm run format:check   # also the Husky pre-commit hook
npm run lint           # htmlhint + stylelint + cspell; also lint:a11y, lint:links (build first)
```

No tests. The pre-commit hook runs `format:check` and the three lints; add legitimate names to `cspell.json` `words` rather than editing copy. Node `26.13.0` per `.nvmrc`; `engines` is `>=26` with `engine-strict=true`.

## Structure

- `src/pages/`: `index.html`, `linkinbio.html` (its own `linkinbio/linkinbio.css`, linked directly). Header/footer are duplicated per page.
- `src/style.css` is the bundle entry, `src/styles/*.css` one concern per file. A new stylesheet only applies once it is `@import`ed there.
- `src/public/`: `robots.txt` (blocks AI crawlers), `sitemap.xml` (`/`, `/linkinbio`), `.well-known/security.txt`, images under `assets/`, committed bootstrap-icons fonts in `fonts/`.
- JSON-LD exists on `linkinbio.html` only. There is no CSP `<meta>`.

## Known issues

- bootstrap-icons fonts are both committed in `src/public/fonts/` and copied from `node_modules` via `externals`; one source should go.

## Deploy

Push to `main` builds and rsyncs `dist/` to production over SSH (`.github/workflows/deploy.yml`), no staging. Work happens on `develop`. CI reads the Node version from `.nvmrc`.

## Scope

@SCOPE.md
