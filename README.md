# Cursor Lint Action

Lint your Cursor `.mdc` and `.cursorrules` files in CI. Catches silent failures before they reach your team.

## What it catches

- Missing YAML frontmatter (silent failure — rules don't load)
- Malformed YAML (silent failure — no warning, no error)
- Missing `alwaysApply: true` (rules ignored in agent mode)
- Missing descriptions (agent can't trigger the rule)
- Vague rules ("follow best practices" has zero effect)
- Bad glob syntax

Based on [real testing](https://dev.to/nedcodes/what-i-actually-put-in-my-project-context-files-1de3) across Sonnet 4.5, Gemini 3 Flash, and GPT-5.1 Codex Mini.

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
| `verify` | Run `--verify` mode (check code against rule patterns) | `false` |
| `version` | cursor-lint version | `latest` |

## Examples

### Lint a specific directory

```yaml
- uses: nedcodes-ok/cursor-lint-action@v1
  with:
    directory: './packages/frontend'
```

### Verify code follows rules

```yaml
- uses: nedcodes-ok/cursor-lint-action@v1
  with:
    verify: true
```

### Pin a version

```yaml
- uses: nedcodes-ok/cursor-lint-action@v1
  with:
    version: '0.3.1'
```

## Why use this

Two out of seven ways an `.mdc` file can be malformed cause **silent failures**. No warning, no error — the rule just doesn't load. In a team setting, one bad commit can break everyone's AI rules without anyone noticing.

This action catches those in CI so they never merge.

## Need a deeper review?

This action catches structural issues. For a full review of your rules, project structure, and model settings — [$50 async setup audit](https://nedcodes.gumroad.com/l/cursor-setup-audit). Written report with specific fixes.

## Links

- [cursor-lint CLI](https://github.com/nedcodes-ok/cursor-lint)
- [VS Code extension](https://open-vsx.org/extension/nedcodes/cursor-lint)
- [npm](https://www.npmjs.com/package/cursor-lint)
- [Free rules collection](https://github.com/nedcodes-ok/cursorrules-collection)

## License

MIT
