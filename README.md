# Setup tenv GitHub Action

A GitHub Action to set up [tofuutils/tenv](https://github.com/tofuutils/tenv) with caching and signature verification support.

## Overview

This action installs tenv, a tool for managing infrastructure tool versions, along with a specified tool (such as Terraform or OpenTofu) with a specific version. It includes caching capabilities and signature verification to ensure the authenticity of downloaded binaries.

## Versioning

This action uses **immutable releases** with full semantic versioning (`vMAJOR.MINOR.PATCH`). Floating major tags (e.g., `v1`) are **not** provided.

When referencing this action, either use the full version string or pin to a commit SHA:

```yaml
# Full version string
uses: rsclarke/setup-tenv@v1.0.0

# Pinned to SHA (recommended)
uses: rsclarke/setup-tenv@<COMMIT_SHA> # v1.0.0
```

## Usage

```yaml
steps:
  - name: Set up OpenTofu
    uses: rsclarke/setup-tenv@v1.0.0
    with:
      tool: tofu
      tool-version: 1.11.5
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `tenv-version` | Version of tenv to install (e.g., `v4.9.3`). | No | v4.9.3 |
| `tool` | Tool to install using tenv (e.g., `terraform`, `tofu`, etc.) | Yes | N/A |
| `tool-version` | Version of the tool to install. | Yes | N/A |

## How It Works

The action:

1. Checks for cached versions of cosign and tenv before downloading
2. Installs cosign using [sigstore/cosign-installer](https://github.com/sigstore/cosign-installer) (version managed by the installer)
3. Downloads and verifies tenv using cosign
4. Installs the specified tool with the specified version using tenv

## Examples

### Installing OpenTofu

```yaml
steps:
  - name: Set up OpenTofu
    uses: rsclarke/setup-tenv@v1.0.0
    with:
      tool: tofu
      tool-version: 1.11.5
```

### Installing Terraform with specific tenv version

```yaml
steps:
  - name: Set up Terraform
    uses: rsclarke/setup-tenv@v1.0.0
    with:
      tenv-version: 4.9.3
      tool: terraform
      tool-version: 1.14.7
```
