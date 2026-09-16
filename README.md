<p align="center">
  <img src="https://raw.githubusercontent.com/Coccinella-Labs/prune/main/.github/assets/thumbnail.png" alt="prune" width="100%">
</p>

# PRune

[![Release](https://img.shields.io/github/v/release/coccinella-labs/prune?logo=github&label=latest)](https://github.com/coccinella-labs/prune/releases)

Write PR descriptions from the actual PR diff.

## What it does

- Shows the base branch SHA before the PR
- Shows the head branch SHA after the PR
- Lists changed files with status and line counts
- Links to the GitHub compare view

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

## Example

**Output:**
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

## License

MIT
