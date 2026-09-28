# claude-skills — context for the model

This plugin ships 5 skills. Here is their intended relationship:

## Skill map

| Skill | When to use |
|---|---|
| `readme` | Default entry point for any README task. Detects project type, then delegates. |
| `extension-page` | VS Code extension only. README.md = Marketplace product page for end users. DEV.md = developer guide. |
| `generate-readme` | All other projects (libraries, CLIs, web apps, APIs, data science). Full README with badges, installation, contributing, license. |
| `create-pr` | Open a GitHub PR with a structured `[PREFIX-N]: [Type] Title Case` title and clean bullet-point body. Uses GitHub MCP, never `gh` CLI. |
| `release` | Bump the project version on the current branch, then (after PR merge) push the release tag from main. |

## Routing rule

Always start with `readme` for README tasks unless the user explicitly invokes `extension-page` or `generate-readme` directly. `readme` is the router — it never duplicates logic, it delegates.

## Hard constraints that apply across all skills

- Never add `Co-Authored-By` or any AI attribution to commit messages.
- Never commit or push without the user reviewing the diff first.
- Never use `gh` CLI for PR creation — always use `mcp__github__create_pull_request`.
- Marketplace README.md has no badges, no Contributing section, no License section — those appear in the VS Code Marketplace sidebar automatically.
