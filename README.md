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

When `cv.pdf` changes, the workflow also syncs the rendered PDF to
`joelnitta/joelnitta-home` at `content/pdf/Nitta_CV.pdf`.

This cross-repo sync uses an additional repository secret:

- `GH_PAT`: Personal Access Token that can push to `joelnitta/joelnitta-home`

Manual run:

1. Open the Actions tab in GitHub.
2. Select the `Render CV` workflow.
3. Click `Run workflow`.

## PAT Rotation (when `GH_PAT` expires)

If the token expires or is revoked, recreate it and update the secret.

Create a new token:

1. Go to GitHub Settings -> Developer settings -> Personal access tokens.
2. Create a fine-grained token (recommended).
3. Repository access: `Only select repositories` -> `joelnitta-home`.
4. Repository permissions: `Contents` -> `Read and write`.
5. Set an expiration date and copy the token value.

Update secret in this repo (`joelnitta-cv`):

1. Go to Settings -> Secrets and variables -> Actions.
2. Edit `GH_PAT` and paste the new token.
3. Save.

Verify after rotation:

1. Run the `Render CV` workflow manually (`workflow_dispatch`) or push a small
	commit.
2. Confirm job success in `joelnitta-cv` Actions.
3. Confirm a commit appears in `joelnitta-home` updating
	`content/pdf/Nitta_CV.pdf`.