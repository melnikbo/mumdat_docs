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

## GitHub Pages setup (required before first deploy)

The **deploy** job returns **404** until Pages is enabled for **GitHub Actions** (not "Deploy from a branch").

1. Open **Settings -> Pages** for your repo, e.g.  
   https://github.com/melnikbo/mumdat_docs/settings/pages
2. Under **Build and deployment**, set **Source** to **GitHub Actions** (not a branch).
3. Save. You do **not** need to pick `main` / `/ (root)` when using Actions.
4. Re-run the workflow: **Actions -> Build and deploy DocFX -> Re-run all jobs**.

After the first successful deploy, the site URL is shown on the **deploy** job and on the **Pages** settings page, typically:

`https://melnikbo.github.io/mumdat_docs/`

### If deploy still fails with 404

- Confirm the repo is **public**, or that your plan allows Pages on private repos.
- Confirm **Settings -> Actions -> General -> Workflow permissions** allows **Read and write** (needed for `GITHUB_TOKEN` and Pages).
- Wait 1-2 minutes after enabling Pages, then re-run (first-time provisioning can lag).

### Node.js 20 warnings

Warnings about Node.js 20 vs 24 on `actions/checkout` / `deploy-pages` are **not** the cause of the 404. They can be ignored for now.

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

Then complete **GitHub Pages setup** above before expecting a green deploy.

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
