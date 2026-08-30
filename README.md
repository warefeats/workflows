# warefeats/workflows

Reusable GitHub Actions workflows for the warefeats org. All warefeats repos are Bun + TypeScript; this repo holds the shared CI building blocks so each benchmark repo stays minimal.

## bun-verify

A reusable workflow that runs the standard Bun verification pipeline: install, typecheck, test, and optionally a smoke command and/or build step.

### Inputs

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `bun-version` | string | `1.4.0` | Bun version to install |
| `smoke-command` | string | `""` | Shell command to run after tests; skipped when empty |
| `build` | boolean | `false` | Run `bun run build` after tests |
| `runs-on` | string | `ubuntu-latest` | Runner label |

### Example caller

```yaml
name: CI

on:
  pull_request:
    branches: [main]
  push:
    branches: [main]

jobs:
  verify:
    uses: warefeats/workflows/.github/workflows/bun-verify.yml@main
    with:
      smoke-command: bun run smoke -- --output=/tmp/smoke.json
```
