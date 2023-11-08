# poetry-pre-commit-cache

This repo contains a action to run various Python tools including:

* [poetry](https://python-poetry.org/docs/)
* [pre-commit](https://pre-commit.com/)
* [TFlint](https://github.com/terraform-linters/tflint)

based on the `.pre-commit-configuration.yaml` and poetry setup.

## Usage

```
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
