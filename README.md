# The Foreman GitHub Actions

This repository contains [reusable workflows](https://docs.github.com/en/actions/learn-github-actions/reusing-workflows)
to reduce duplication in actions in the Foreman project.

## Rubocop

To call Rubocop within your CI, use the following workflow:

```yaml
name: CI

on: pull_request

concurrency:
  group: ${{ github.head_ref }}
  cancel-in-progress: true

jobs:
  rubocop:
    name: Rubocop
    uses: ekohl/actions/.github/workflows/rubocop.yml@v0
```
