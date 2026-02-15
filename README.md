# Agentic Security Action

A GitHub Action for scanning GitHub Actions workflows for security vulnerabilities.

## Usage

```yaml
name: Security Scan
on: [push, pull_request]

jobs:
  security-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: yksanjo/agentic-security-action@v1
        with:
          path: '.github/workflows'
          severity: 'HIGH'
```

## Inputs

| Input | Description | Default |
|-------|-------------|---------|
| path | Path to scan | `.github/workflows` |
| severity | Minimum severity level | `HIGH` |
| format | Output format (text, json) | `text` |

## Example with Fail on Critical

```yaml
name: Security Scan
on: [push, pull_request]

jobs:
  security-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: yksanjo/agentic-security-action@v1
        with:
          path: '.github/workflows'
          severity: 'HIGH'
          format: 'json'
```

## Detects

- Overly permissive GitHub token permissions
- pull_request_target usage
- Dangerous shell commands (rm -rf, eval, curl | sh)
- Hardcoded secrets (GitHub PAT, AWS keys, API keys)
