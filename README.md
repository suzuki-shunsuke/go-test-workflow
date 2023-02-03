# go-test-workflow

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
    uses: suzuki-shunsuke/go-test-workflow/.github/workflows/test.yaml@fc631d6d1b9b19730fc20dcde15966497469d7fe # v0.1.1
    with:
      aqua_policy_config: aqua-policy.yaml
      aqua_version: v1.32.3
    permissions:
      pull-requests: write
      contents: read # To checkout private repository
```

## Workflow

[Workflow](.github/workflows/test.yaml)

## Requirements

- reviewdog
- golangci-lint

```sh
aqua g -i reviewdog/reviewdog golangci/golangci-lint
```

## LICENSE

[MIT](LICENSE)
