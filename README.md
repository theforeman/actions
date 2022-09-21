# The Foreman GitHub Actions

This repository contains [reusable workflows](https://docs.github.com/en/actions/learn-github-actions/reusing-workflows)
to reduce duplication in actions in the Foreman project.

At this moment it's considered experimental.

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
    uses: theforeman/actions/.github/workflows/rubocop.yml@v0
```

## Foreman plugin tests

To run the Foreman tests once Rubocop has passed, use the following workflow:

```yaml
name: CI

on: pull_request

concurrency:
  group: ${{ github.head_ref }}
  cancel-in-progress: true

jobs:
  rubocop:
    name: Rubocop
    uses: theforeman/actions/.github/workflows/rubocop.yml@v0

  test:
    name: Ruby
    needs: rubocop
    uses: theforeman/actions/.github/workflows/foreman_plugin.yml@v0
    with:
      plugin: MY_PLUGIN
```

## Gem release

To release a gem, use the following workflow

```yaml
name: Release

on:
  create:
    ref_type: tag

jobs:
  release:
    name: Release gem
    uses: theforeman/actions/.github/workflows/release-gem.yml@v0
    with:
      allowed_owner: MY_USERNAME
    secrets:
      api_key: ${{ secrets.RUBYGEM_API_KEY }}
```
