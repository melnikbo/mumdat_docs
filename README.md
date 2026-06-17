# handbook-docfx-starter

Minimal DocFX docs repo (mumdat.github.io/docs style) for **product** handbooks.
Use this folder as the root of a new GitHub repository and push to GitHub Pages.

## Layout

```
handbook-docfx-starter/
  docfx.json
  de-de/
    index.md
    toc.yml
    docs/mmplus/arbeitsvorstahl/arbeitsvorstahl.md
  images/
  public/main.css
  configs/handbook_docfx_paths.example.json
  .github/workflows/docfx.yml
```

Published URL pattern (project site):

`https://<user>.github.io/<repo>/de-DE/docs/mmplus/arbeitsvorstahl/arbeitsvorstahl.html`

## Initial push

```bash
cd handbook-docfx-starter

git init
git add .
git commit -m "Initial DocFX docs site structure"

# create empty repo on GitHub first, then:
git remote add origin git@github.com:<YOUR_USER>/<YOUR_DOCS_REPO>.git
git branch -M main
git push -u origin main
```

## GitHub Pages setup

1. Repo **Settings** -> **Pages** -> **Build and deployment** -> Source: **GitHub Actions**
2. After the first push, open **Actions** -> workflow **Build and deploy DocFX**
3. When green, open the Pages URL from the deploy job

## Local preview (optional)

Requires [.NET SDK 8+](https://dotnet.microsoft.com/download):

```bash
dotnet tool install -g docfx
docfx docfx.json
docfx serve _site
# open http://localhost:8080
```

## Project site base path

If links/CSS break on GitHub Pages (repo is not `username.github.io` root), set in `docfx.json` under `globalMetadata`:

```json
"_appBasePath": "/YOUR_DOCS_REPO/"
```

Replace `YOUR_DOCS_REPO` with the GitHub repository name.

## Adding modules

1. Add `de-de/docs/<productLine>/<moduleSlug>/<moduleSlug>.md`
2. Add entry to `de-de/toc.yml`
3. Push -> CI rebuilds the site

See `configs/handbook_docfx_paths.example.json` for a future BlackBox push mapping.

## Relation to BlackBox

| Repo type | Handbook delivery |
|-----------|-------------------|
| Product (`idRanges` >= 1M) | This DocFX repo (planned auto-push from worker) |
| Client (`idRanges` < 1M) | `docs/handbook.md` in client AL repo (`blackbox/handbook-docs` branch) |
