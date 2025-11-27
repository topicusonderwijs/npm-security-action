# NPM security action

This action allows you to scan you project for known `security` vulnerabilities. This is done using several "free" as "paid" tools

| Tool       | License                 | Link                |
| ---------- | ----------------------- | ------------------- |
| NPM audit  | Free                    | -                   |
| Audit CI   | Free                    | -                   |
| Trivy      | Free                    | https://trivy.dev/  |
| Socket.dev | Free (with limitations) | https://socket.dev/ |
| Snyk       | Paid                    | https://snyk.io/    |

## Package managers

The action comes with build in support for different package managers

- PNPM
- NPM
- Yarn

## Example

Include a step in your Github workflow

```yml
name: Security Scan

on:
  push:
    branches:
      - main
  workflow_dispatch:

jobs:
  security-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: topicusonderwijs/npm-security-action@v1
        with:
          package-manager: pnpm
          severity-threshold: high
          working-directory: .
          enable-pr-comments: true
          snyk-token: ${{ secrets.SNYK_TOKEN }}
```

## Settings

Below settings are available to configure your action

| Setting            | Description                      | Required | Default  | Values                        |
| ------------------ | -------------------------------- | -------- | -------- | ----------------------------- |
| node-version       | Node.js version to use           | yes      | 24       | 20, 22, 24                    |
| package-manager    | Package manager to use           | yes      | npm      | npm, pnpm, yarn               |
| severity-threshold | Minimum severity level to report | yes      | moderate | low, moderate, high, critital |
| working-directory  | Working directory for the scan   | yes      | .        | valid path                    |
| enable-pr-comments | Enable automatic PR comments     | no       | true     | true, false                   |
| socket-token       | Socket.dev API token             | no       | null     | valid apikey                  |
| snyk-token         | Snyk API token                   | no       | null     | valid apikey                  |
