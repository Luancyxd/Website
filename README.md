# Website

Static landing site with no analytics, cookies, backend, or third-party
JavaScript. It contains the product landing page, a captured Web Radar preview,
profile downloads, and the HTML build of the Lua API documentation.

## Local preview

```powershell
cd website
npm run build
npm run serve
```

Open `http://127.0.0.1:4173/`. Do not open `index.html` through a `file://` URL:
Firefox blocks the radar preview's JSON requests for local files.

The build copies:

- the feature catalogue from `website/feature-tree-data.js`;
- profiles that exist in `configs/`;
- `lua/scripts/Web Radar.lua`;
- Markdown documentation from `lua/docs`.

Missing profiles are rendered as unavailable instead of producing broken links.
Edit `site-config.js` only when explicit release/source URLs are required.

## Deploy

The site is static, so it can be published straight from the repository. The
build configuration lives in `vercel.json` at the repository root, which is why
the commands below run from the root rather than from `website/`.

With the Vercel CLI, no Git remote is required:

```powershell
npx vercel login
npx vercel --prod
```

Alternatively, push the repository to GitHub and import it at
<https://vercel.com/new>. Vercel then rebuilds and redeploys on every push.

`.vercelignore` keeps the upload small by excluding `build/` and the native
sources, which the static site does not read. Only `website/`, `configs/`,
`lua/docs/` and `lua/scripts/` are needed at build time.
