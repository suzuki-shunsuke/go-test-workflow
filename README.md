# go-test-workflow

[![Ask DeepWiki](https://deepwiki.com/badge.svg)](https://deepwiki.com/suzuki-shunsuke/go-test-workflow)
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
    uses: suzuki-shunsuke/go-test-workflow/.github/workflows/test.yaml@a35526722b39d5f64145e8fa0af22a68db1fd9d4 # v2.0.1
    with:
      aqua_policy_config: aqua-policy.yaml
      aqua_version: v2.59.1
      go-version: 1.26.2
      golangci-lint-timeout: 120s
    permissions:
      pull-requests: write
      contents: read # To checkout private repository
      id-token: write # For takumi guard
```

## Workflow

[Workflow](.github/workflows/test.yaml)

## Requirements

- reviewdog
- golangci-lint
- goreleaser if `.goreleaser.yml` or `.goreleaser.yaml` exists
- go-licenses

```sh
aqua g -i reviewdog/reviewdog golangci/golangci-lint goreleaser/goreleaser google/go-licenses
```

## LICENSE

[MIT](LICENSE)
