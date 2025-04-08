# Setup tenv GitHub Action

A GitHub Action to set up [tofuutils/tenv](https://github.com/tofuutils/tenv) with caching and signature verification support.

## Overview

This action installs tenv, a tool for managing infrastructure tool versions, along with a specified tool (such as Terraform or OpenTofu) with a specific version. It includes caching capabilities and signature verification to ensure the authenticity of downloaded binaries.

## Usage

```yaml
steps:
  - name: Set up OpenTofu
    uses: rsclarke/setup-tenv@v1
    with:
      tool: tofu
      tool-version: 1.6.0
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `cosign-version` | Version of cosign to install (e.g., `v2.5.0`). | No | v2.5.0 |
| `tenv-version` | Version of tenv to install (e.g., `v4.4.0`). | No | v4.4.0 |
| `tool` | Tool to install using tenv (e.g., `terraform`, `tofu`, etc.) | Yes | N/A |
| `tool-version` | Version of the tool to install. | Yes | N/A |

## How It Works

The action:

1. Checks for cached versions of cosign and tenv before downloading
2. Installs cosign (with optional version specification)
3. Downloads and verifies tenv using cosign
4. Installs the specified tool with the specified version using tenv

## Examples

### Installing OpenTofu

```yaml
steps:
  - name: Set up OpenTofu
    uses: rsclarke/setup-tenv@v1
    with:
      tool: tofu
      tool-version: 1.6.0
```

### Installing Terraform with specific tenv version

```yaml
steps:
  - name: Set up Terraform
    uses: rsclarke/setup-tenv@v1
    with:
      tenv-version: 4.4.0
      tool: terraform
      tool-version: 1.7.1
```
