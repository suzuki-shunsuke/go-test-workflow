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
    uses: suzuki-shunsuke/go-test-workflow/.github/workflows/test.yaml@287a75bd5ffae8d64db887708d9262381a7f6655 # v1.1.1
    with:
      aqua_policy_config: aqua-policy.yaml
      aqua_version: v1.32.3
      go-version: 1.19.5
      golangci-lint-timeout: 120s
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
