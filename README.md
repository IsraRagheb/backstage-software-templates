# Backstage Python Flask Template

This repository is a [Backstage](https://backstage.io/) software template. It scaffolds a small Flask service, publishes it to GitHub, and registers the new component in the Backstage catalog.

Use it from Backstage Software Templates. When you run the template, you provide a component name and an environment (`dev` or `prod`). The scaffolder copies the files in this repo, substitutes `${{ values.* }}` placeholders, creates a public GitHub repository, and registers `catalog-info.yaml`.

## Repository layout

`template.yaml` is the Backstage template definition (parameters and scaffolder steps). Everything else is the skeleton copied into each new service:

| Path | Purpose |
| --- | --- |
| `src/` | Flask app: home page, `/api/v1/info`, and `/api/v1/healthz` |
| `Dockerfile` | Python 3.10 Alpine image for the app |
| `catalog-info.yaml` | Backstage Component metadata and TechDocs |
| `charts/` | Helm chart for the app, plus Argo CD values |
| `k8s/` | Raw Kubernetes manifests |
| `.github/workflows/` | CI/CD: build and push an image, then sync with Argo CD |
| `docs/` and `mkdocs.yaml` | TechDocs for the generated service |

## How it works

1. **Fetch** — `fetch:template` copies this repository and fills in `app_name` and `app_env`.
2. **Publish** — `publish:github` creates the new repo.
3. **Register** — `catalog:register` adds the component to the Backstage catalog.

Point Backstage at this repository (or at `template.yaml`) as a template location so it shows up in the Templates catalog.
