# HoundDog.ai GitHub Action

## Overview

HoundDog.ai's code scanner is designed to proactively detect issues related to sensitive data mishandling and leakages
early in the development cycle. By using the application’s source code as the source of truth, security teams can ensure
data security controls are integrated from the start, rather than later when the data is already in production. This
shift-left approach reduces the risk of breaches from issues involving sensitive data being stored in logs, files,
tokens, cookies, or when shared through APIs and with third-party systems.

## Supported Programming Languages

* Java
* SQL
* GraphQL
* OpenAPI / Swagger

## Inputs

| Name              | Description                                                          | Default          |
|-------------------|----------------------------------------------------------------------|------------------|
| `output_format`   | Output format. Allowed values are `console`, `markdown` and `sarif`. | `sarif`          |
| `output_filename` | Output filename. Not applicable for the `console` output format.     | `hounddog.sarif` |

For more configuration options, please see the [HoundDog.ai documentation](https://docs.hounddog.ai).

## Example

The following GitHub Actions workflow runs a HoundDog.ai scan on pull requests and uploads the results to GitHub
Advanced Security:

```yaml
name: HoundDog.ai Scan
on:
  pull_request:
    branches: [ main ]
jobs:
  hounddog:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      security-events: write
    steps:
      - name: Checkout repository
        uses: actions/checkout@master

      - name: Run HoundDog.ai scan
        uses: hounddogai/hounddog-action@v1
        with:
          output_format: sarif
          output_filename: hounddog.sarif

      - name: Upload scan results to GitHub Advanced Security
        uses: github/codeql-action/upload-sarif@v2
        with:
          sarif_file: hounddog.sarif
```

If you need any help or would like to send us feedback, please shoot us an email
at [support@hounddog.ai](mailto:support@hounddog.ai).
