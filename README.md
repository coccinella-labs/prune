<p align="center">
  <img src="https://raw.githubusercontent.com/Coccinella-Labs/prune/main/.github/assets/thumbnail.png" alt="prune" width="100%">
</p>

# PRune

[![Release](https://img.shields.io/github/v/release/coccinella-labs/prune?logo=github&label=latest)](https://github.com/coccinella-labs/prune/releases)

Write PR descriptions from the actual PR diff.

## What it does

- Reads the repository's own PR template and treats its headings as the required sections
- Leaves a description alone once it already satisfies that template
- Otherwise scaffolds the description to the template headings, with the changed-file table filled in
- Shows the base branch SHA before the PR, the head branch SHA after it, and the compare link
- Falls back to the plain `Summary` / `Changes` format when the repository has no PR template

Bodies are never destroyed: if a description already covers every template heading, PRune is a no-op.

## Trigger

Automatically on PR: `opened`, `edited`, `ready_for_review`

## Usage

```yaml
name: Normalize PR

on:
  pull_request_target:
    types: [opened, edited, ready_for_review]

jobs:
  normalize:
    runs-on: ubuntu-latest
    steps:
      - uses: coccinella-labs/prune@v1
```

## Inputs

| Input | Default | Description |
| --- | --- | --- |
| `overwrite` | `false` | Rewrite the description even when it already satisfies the template |
| `template-paths` | `.github/pull_request_template.md,.github/PULL_REQUEST_TEMPLATE.md` | Comma-separated template paths to look for, in order |

## Example

**No PR template in the repository (fallback format):**

```
## Summary
Example PR title

## Changes
| File | Status | Additions | Deletions |
| --- | --- | --- | --- |
| `action.yml` | modified | 12 | 4 |
| `README.md` | modified | 8 | 20 |

## Base
`main` at `abc1234`

## Head
`fix/example` at `def5678`

## Compare
https://github.com/owner/repo/compare/abc1234...def5678

---
<img src="https://avatars.githubusercontent.com/u/283287531?s=16" width="16" alt=""> `coccinella-labs/prune@v1`
```

**With a template whose headings are `## Changes` and `## Validation`:**

```
## Changes

| File | Status | Additions | Deletions |
| --- | --- | --- | --- |
| `action.yml` | modified | 12 | 4 |
| `README.md` | modified | 8 | 20 |

## Validation

_List the exact commands or manual checks used._

## Base
`main` at `abc1234`
...
```

## License

MIT
