# VS Code Marketplace Page Examples

These are the canonical reference pages to fetch when researching how to structure an extension's Marketplace listing.

## Best-in-class examples (fetch these)

| Extension | URL | What to study |
|-----------|-----|---------------|
| CodeRabbit | `https://marketplace.visualstudio.com/items?itemName=CodeRabbit.coderabbit-vscode` | Hook-first structure, GIF placement, no badges |
| GitLens | `https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens` | Progressive disclosure, feature-per-image layout, length |
| Error Lens | `https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens` | Minimal but effective, single early image |
| Draw.io | `https://marketplace.visualstudio.com/items?itemName=hediet.vscode-drawio` | Visual-first, very short prose |
| Code Spell Checker | `https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker` | Configuration table style |

## Key patterns extracted from top extensions

**Opening hook:**
- Lead with the problem or the moment of friction (not the feature list)
- 2–3 sentences max before the first visual
- CodeRabbit example: "AI coding tools let you write 10x faster. But reviews still happen days later in PRs. CodeRabbit reviews your code instantly in VS Code..."

**Badges:**
- Top extensions do NOT use CI/version/license badge rows
- The Marketplace sidebar already shows: version, last updated, install count, rating, license, publisher
- Badges clutter the listing and signal "developer README", not "product page"

**Features section:**
- Bold headline + em dash + one sentence of user benefit (not "easy to use" vagueness)
- GIF or screenshot immediately after the feature description it illustrates
- Each GIF shows ONE thing — no cramming multiple features into one recording

**Installation:**
- Primary: search in Extensions panel by display name
- Secondary (optional): VSIX install command
- Never mention building from source — that's DEV.md content

**Configuration:**
- Table format: Setting | Default | Description
- List every property from package.json contributes.configuration
- Use the exact setting key users will type in settings.json

**What NOT to include:**
- Badges (CI, version, license)
- Project structure trees
- npm commands (compile, test, lint)
- Architecture explanations
- Contributing guidelines (more than 1 sentence)
- License section (shown in sidebar)
- "How it works" data flow diagrams

## Fetch pattern

```
https://marketplace.visualstudio.com/items?itemName=<publisher>.<extension-id>
```

Fetch the Marketplace URL (not raw GitHub README) — the Marketplace renders differently and shows what users actually see. Relative image paths work because vsce bundles the assets/ folder.
