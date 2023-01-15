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
    uses: suzuki-shunsuke/go-test-workflow/.github/workflows/test.yaml@fc631d6d1b9b19730fc20dcde15966497469d7fe # v0.1.1
    with:
      aqua_policy_config: ${{ env.AQUA_POLICY_CONFIG }}
    permissions:
      pull-requests: write
```

## Requirements

- reviewdog
- golangci-lint

```sh
aqua g -i reviewdog/reviewdog golangci/golangci-lint
```

## LICENSE

[MIT](LICENSE)
