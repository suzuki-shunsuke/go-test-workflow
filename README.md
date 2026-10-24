# go-test-workflow

[Workflow](.github/workflows/test.yaml)

GitHub Actions Reusable Workflow for testing Go application

## How to use

```yaml
---
name: test
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
permissions: {}
jobs:
  test:
    uses: suzuki-shunsuke/go-test-workflow/.github/workflows/test.yaml@f0dafddd9f9075a33e4ff40a44bdabd79335e7a3 # v3.1.1
    with:
      aqua_policy_config: aqua-policy.yaml
      aqua_version: v2.63.0
      go-version-file: go.mod
      golangci-lint-timeout: 120s
    permissions:
      pull-requests: write
      contents: read # To checkout private repository
      id-token: write # For takumi guard
```

### Share Go modules with other jobs

By default, the workflow downloads Go modules in its own job.
If you want to share Go modules with other jobs such as integration tests, download them with [download-go-module-action](https://github.com/suzuki-shunsuke/download-go-module-action) in the caller workflow and pass the artifact name via `gomodule_artifact_name`.
Then the workflow skips downloading Go modules.
The artifact must include go-licenses.

```yaml
jobs:
  gomodule:
    uses: suzuki-shunsuke/download-go-module-action/.github/workflows/download.yaml@5d7ee96c505de1e3265c2d5ad67d2c66076844f1 # v0.0.9
    permissions:
      contents: read
      id-token: write
    with:
      aqua_version: v2.64.0
      aqua_packages: go-licenses
    secrets:
      TAKUMI_GUARD_BOT_ID: ${{secrets.TAKUMI_GUARD_BOT_ID}}

  test:
    needs: [gomodule]
    uses: suzuki-shunsuke/go-test-workflow/.github/workflows/test.yaml@f0dafddd9f9075a33e4ff40a44bdabd79335e7a3 # v3.1.1
    with:
      aqua_version: v2.64.0
      go-version-file: go.mod
      gomodule_artifact_name: gomodule
    permissions:
      pull-requests: write
      contents: read # To checkout private repository
      id-token: write # The skipped gomodule job still requires this permission
```

## Workflow

[Workflow](.github/workflows/test.yaml)

## Requirements

- golangci-lint
- goreleaser if `.goreleaser.yml` or `.goreleaser.yaml` exists
- reviewdog (optional)
- go-licenses (optional)

```sh
aqua g -i reviewdog/reviewdog golangci/golangci-lint goreleaser/goreleaser google/go-licenses
```
