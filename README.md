# AutoCat Docker Builder

This public repository contains the manual GitHub Actions workflow used to build
the Docker image for the private [uifor/AutoCat](https://github.com/uifor/AutoCat)
repository.

The source repository is checked out only inside the temporary GitHub-hosted
runner. It is not copied into this repository, uploaded as an artifact, or
included in the final image.

## Required repository secrets

Configure these secrets in **Settings -> Secrets and variables -> Actions**:

- `AUTOCAT_READ_TOKEN`: a read-only token that can read the private `uifor/AutoCat`
  repository contents.
- `GHCR_TOKEN`: a token that can publish the `ghcr.io/uifor/autocat` package.

Keep these tokens separate and do not print them from workflow steps. The public
workflow is intentionally limited to manual `workflow_dispatch` runs so that
untrusted pull requests cannot access the secrets.

## Build

Open **Actions -> Docker image -> Run workflow**. The default target is
`linux/arm64`; select `linux/amd64` only when needed.

The workflow builds the frontend and Docker image in one temporary job. It does
not use a GitHub Actions Docker layer cache, because intermediate layers can
contain private source files.
