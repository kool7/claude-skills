# claude-skills

Personal Claude Code skills for everyday development workflows.

## Skills

| Skill | Description |
|-------|-------------|
| `create-pr` | Create a GitHub PR with structured title format and clean description |
| `extension-page` | Write a VS Code Marketplace listing page (README.md) for an extension |
| `generate-readme` | Generate a full README.md for any non-extension GitHub project |
| `readme` | Smart README - auto-detects project type and applies the right rules |
| `release` | Bump version and push release tag after merge |

## Install

Add this to your `~/.claude/settings.json`:

```json
"extraKnownMarketplaces": {
  "kool7-skills": {
    "source": {
      "source": "github",
      "repo": "kool7/claude-skills"
    },
    "autoUpdate": true
  }
},
"enabledPlugins": {
  "claude-skills@kool7-skills": true
}
```

## Usage

```
/create-pr
/readme
/generate-readme
/extension-page
/release
```

## License

MIT
