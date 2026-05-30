# joelnitta-cv

Repo for generating [Joel Nitta](https://www.joelnitta.com)'s CV.

Based on [quarto-awesomecv-typst](https://github.com/kazuyanagimoto/quarto-awesomecv-typst) template.

## Dependencies

Requires [quarto](https://quarto.org/) and R.

R dependencies are pinned with `renv`.

Local setup:

```r
renv::restore()
```

For local rendering, provide these environment variables:

- `ZOTERO_API_KEY`
- `ZOTERO_USER_ID`

## Rendering

Render CV:

```
quarto render cv.qmd
```

## Automated Rendering

GitHub Actions renders the CV automatically:

- On push to `main`
- On a nightly schedule
- On manual dispatch

The workflow reads repository secrets `ZOTERO_API_KEY` and `ZOTERO_USER_ID`,
renders `cv.qmd`, and commits `cv.pdf` back to `main` only if the PDF changed.

Manual run:

1. Open the Actions tab in GitHub.
2. Select the `Render CV` workflow.
3. Click `Run workflow`.