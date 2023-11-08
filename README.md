# poetry-pre-commit-cache

This repo contains an action to install and cache the following tools:

* [poetry](https://python-poetry.org/docs/)
* [pre-commit](https://pre-commit.com/)
* [TFlint](https://github.com/terraform-linters/tflint)

The cache is determined primarily by `poetry.lock` and `.pre-commit-configuration.yaml`.

## Inputs

```yaml
inputs:
  python-version:
    description: |
      Python version to use
      Default is 3.9.
    required: true
    default: '3.9'
  poetry-version:
    description: |
      Poetry version to use
      Default is 1.4.2.
    required: true
    default: '1.4.2'
  hooks-to-skip:
    description: |
      pre-commit hooks to skip
      should be passed with the comma separator
      e.g.: sqlfluff-fix,sqlfluff-lint,terraform_fmt,terrascan
      Default is run all pre-commit hooks.
    required: false
    default: ''
  cache-paths:
    description: |
      A list of files, directories, and wildcard patterns to cache.
      Default are .venv, ~/.local and ~/.cache/pre-commit.
    required: true
    default: |
        .venv
        ~/.local
        ~/.cache/pre-commit
  tflint-version:
    description: |
      The version of TFlint to install
      Default is v0.48.0.
    required: false
    default: v0.48.0
```

## Usage

```yaml
name: Pull Request
on:
    push:
        branches: [ main ]
    pull_request:
        branches: [ main ]
    workflow_dispatch:

jobs:
    pre-commit:
        runs-on: ubuntu-latest
        steps:
            - name: Checkout Code
                uses: actions/checkout@v4
                with:
                    fetch-depth: 0

            - id: pre-commit
              uses: Kristina-Pianykh/poetry-pre-commit-cache@main
              with:
                  python-version: '3.10'
                  poetry-version: '1.4.2'
```
