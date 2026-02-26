# Cursor Lint Action

> ⚠️ **This action now uses [cursor-doctor](https://github.com/nedcodes-ok/cursor-doctor)** — the evolution of cursor-lint with broader diagnostics and auto-fix.

Lint your Cursor `.mdc` and `.cursorrules` files in CI. Catches silent failures before they reach your team.

## What it catches

- Missing YAML frontmatter (silent failure — rules don't load)
- Malformed YAML (silent failure — no warning, no error)
- Missing `alwaysApply: true` (rules ignored in agent mode)
- Missing descriptions (agent can't trigger the rule)
- Vague rules ("follow best practices" has zero effect)
- Bad glob syntax
- Conflicting rules across files

## Usage

```yaml
name: Lint Cursor Rules
on: [push, pull_request]

jobs:
  cursor-lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: nedcodes-ok/cursor-lint-action@v1
```

## Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `directory` | Directory to lint | `.` |
| `version` | cursor-doctor version | `latest` |

## Examples

### Lint a specific directory

```yaml
- uses: nedcodes-ok/cursor-lint-action@v1
  with:
    directory: './packages/frontend'
```

### Pin a version

```yaml
- uses: nedcodes-ok/cursor-lint-action@v1
  with:
    version: '1.1.4'
```

## Why use this

Two out of seven ways an `.mdc` file can be malformed cause **silent failures**. No warning, no error — the rule just doesn't load. In a team setting, one bad commit can break everyone's AI rules without anyone noticing.

This action catches those in CI so they never merge.

## Need deeper diagnostics?

**[cursor-doctor Pro](https://nedcodes.gumroad.com/l/cursor-doctor-pro)** ($9 one-time) — full diagnostic report with conflict detection, redundancy analysis, token budget breakdown, and auto-fix.

## Links

- [cursor-doctor CLI](https://github.com/nedcodes-ok/cursor-doctor)
- [npm](https://www.npmjs.com/package/cursor-doctor)
- [Free rules collection](https://github.com/nedcodes-ok/cursorrules-collection)

## License

MIT
