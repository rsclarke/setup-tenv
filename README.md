# Setup tenv GitHub Action

A GitHub Action to set up [tofuutils/tenv](https://github.com/tofuutils/tenv) with caching and signature verification support.

## Overview

This action installs tenv, a tool for managing infrastructure tool versions, along with a specified tool (such as Terraform or OpenTofu) with a specific version. It includes caching capabilities and signature verification to ensure the authenticity of downloaded binaries.

## Versioning

This action uses **immutable releases** with full semantic versioning (`vMAJOR.MINOR.PATCH`). Floating major tags (e.g., `v1`) are **not** provided.

When referencing this action, either use the full version string or pin to a commit SHA:

```yaml
# Full version string
uses: rsclarke/setup-tenv@<VERSION>

# Pinned to SHA (recommended)
uses: rsclarke/setup-tenv@<COMMIT_SHA> # <VERSION>
```

## Usage

```yaml
steps:
  - name: Set up OpenTofu
    uses: rsclarke/setup-tenv@<VERSION>
    with:
      tool: tofu
      tool-version: 1.11.5
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `tenv-version` | Version of tenv to install (e.g., `v4.9.3`). | No | Latest release |
| `tool` | Tool to install using tenv (e.g., `terraform`, `tofu`, etc.) | Yes | N/A |
| `tool-version` | Version of the tool to install. | Yes | N/A |

## How It Works

The action:

1. Resolves the latest tenv release unless `tenv-version` is explicitly set
2. Restores any cached tenv installation for the requested version
3. Sets up cosign with [rsclarke/setup-cosign](https://github.com/rsclarke/setup-cosign) only when tenv needs to be downloaded and verified
4. Downloads and verifies tenv using cosign
5. Installs the specified tool with the specified version using tenv

## Examples

### Installing OpenTofu

```yaml
steps:
  - name: Set up OpenTofu
    uses: rsclarke/setup-tenv@<VERSION>
    with:
      tool: tofu
      tool-version: 1.11.5
```

### Installing Terraform with specific tenv version

```yaml
steps:
  - name: Set up Terraform
    uses: rsclarke/setup-tenv@<VERSION>
    with:
      tenv-version: 4.9.3
      tool: terraform
      tool-version: 1.14.7
```
