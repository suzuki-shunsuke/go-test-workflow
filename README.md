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
    uses: suzuki-shunsuke/go-test-workflow/.github/workflows/test.yaml@974c826cf99fff2f29b317a45713e2d5731a0c32 # v0.4.0
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
