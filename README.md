![check-file-permissions-action header](https://raw.githubusercontent.com/gi-org-pl/check-file-permissions-action/main/.github/image/header.png)

# check-permissions-action

A GitHub Action that fails if any file permission (mode) changes are introduced in a PR.

## Usage

```yaml
- name: Check for file permission changes
  uses: gi-org-pl/check-permissions-action@v1
  with:
    base-ref: ${{ github.base_ref }}
```

## Inputs

| Input      | Description                    | Required | Default |
|------------|--------------------------------|----------|---------|
| `base-ref` | Base branch to compare against | No       | `main`  |

## Example workflow

```yaml
name: PR Sanity Checks

on:
  pull_request:

jobs:
  check:
    runs-on: ubuntu-24.04
    steps:
      - uses: actions/checkout@v6
        with:
          fetch-depth: 0

      - name: Check for file permission changes
        uses: gi-org-pl/check-permissions-action@v1
        with:
          base-ref: ${{ github.base_ref }}
```

## How it works

The action uses `git diff --summary` to detect any `mode change` entries between the PR branch and the base branch. chmod-style changes like making a file executable (`644 → 755`) will fail the workflow.

## Authors

Action author is [Oskar Barcz](https://github.com/oskarbarcz), CTO of **[Generacja Innowacja](https://gi.org.pl)** —
Poland's first technology-first NGO.

## License

MIT