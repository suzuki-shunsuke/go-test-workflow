# go-test-workflow

GitHub Actions Reusable Workflow for testing Go application

## How to use

```yaml
---
name: test
env:
  AQUA_POLICY_CONFIG: ${{ github.workspace }}/aqua-policy.yaml
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
permissions: {}
jobs:
  test:
    uses: suzuki-shunsuke/go-test-workflow/.github/workflows/test.yaml@e63ffd2de162e7a38c0f1b3ccaba92f9425edb6e # v0.1.0
    permissions:
      pull-requests: write
```

## Requirements

- reviewdog
- golangci-lint

For aqua users,

```sh
aqua g -i reviewdog/reviewdog golangci/golangci-lint
```

## LICENSE

[MIT](LICENSE)
