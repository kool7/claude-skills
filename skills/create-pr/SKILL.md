---
name: create-pr
description: Create a GitHub PR with structured title [PREFIX-N]:[Type] Title Case and clean bullet-point description. Use when the user asks to open, raise, or create a pull request.
allowed-tools: Bash mcp__github__list_pull_requests mcp__github__create_pull_request mcp__github__update_issue
---

# Create Pull Request

## Step 1 — Detect repo and next PR number

Run in parallel using GitHub MCP (never `gh` CLI or git push):
- Get repo owner/name: run `git remote get-url origin` via Bash, parse `github.com/{owner}/{repo}` from the URL
- Get current branch: `git branch --show-current`
- `mcp__github__list_pull_requests` (owner, repo, state: all, per_page: 10) → find the highest PR **number** (the `number` field, not the CV number in the title). Next PR = highest + 1.

**PR title number rule:** The CV number in the title equals the next GitHub PR number. If the last PR was #7, title uses CV-8.

If the user passed a prefix as an argument (e.g. `/create-pr CV`), use it. Otherwise check the project CLAUDE.md for a line like `prefix: CV`. If still not found, ask the user: "What prefix should I use? (e.g. CV, AB, FA)"

## Step 2 — Understand what changed

Read the commits on the current branch that are ahead of main:
```
git log main..HEAD --oneline
```
Also read any description the user gave when invoking the skill. Use both to understand what was done.

## Step 3 — Choose the PR type

Pick exactly one — use the most specific match:

| Type | When |
|------|------|
| `Enhancement` | New feature or meaningful improvement users will notice |
| `Bug Fix` | Fixes broken behavior that users experienced |
| `Fix` | Small targeted fix — single issue, narrow scope |
| `Chore` | CI, tooling, config, version bumps — no user-facing change |
| `Refactor` | Code reorganisation, no behavior change |
| `Docs` | Documentation only |

## Step 4 — Compose the title

```
[{PREFIX}-{N}]: [{Type}] {Title In Title Case}
```

Rules:
- Every word capitalised (Title Case), including prepositions if 4+ letters
- Describes WHAT was done, not HOW — from the user's perspective
- No file names, no function names, no technical internals
- Keep the title portion under 60 characters

Good examples:
```
[CV-8]: [Fix] Windows Path Separator For Line Decorations
[CV-9]: [Enhancement] Auto Run Tests On Missing Coverage
[CV-10]: [Chore] Bump Version To 1.0.0
```

Bad examples (reject these patterns):
```
[CV-8]: [Fix] fix findFileInReport backslash bug   ← lowercase, mentions internal name
[CV-8]: [Fix] Fixed The Windows Path Issue         ← past tense in title, vague
```

## Step 5 — Write the description

- 3–5 bullet points, plain `*` bullets
- Plain English — no file names, no function names, no code
- Each bullet: one concrete thing fixed or added, from the user's perspective
- Start with a past-tense verb: Fixed, Added, Removed, Improved
- No section headers, no bold, no sub-bullets
- No mention of Claude, AI, or any attribution

Good example:
```
* Fixed line highlights not appearing on Windows — coverage paths use forward slashes but Windows editor paths use backslashes, causing the file lookup to silently fail.
* Sidebar and status bar were already correct since they iterate files directly; only the editor decoration lookup was affected.
```

Bad example (reject):
```
## Bug Fix
The `findFileInReport` function was updated to normalize `\\` to `/`...
```

## Step 6 — Create the PR and assign

**6a. Create the PR** using `mcp__github__create_pull_request`:
- `owner` and `repo`: from Step 1
- `head`: current branch (from Step 1)
- `base`: main
- `title`: from Step 4
- `body`: bullets from Step 5

**6b. Immediately after**, call `mcp__github__update_issue` with the PR number returned in step 6a to set assignees and labels in one call:
- `assignees`: `["kool7"]` — always assign the repo owner
- `labels`: pick from the label map below based on the PR type from Step 3

**Label rules — always apply ALL that fit, never just one if multiple apply:**

| Condition | Add label |
|-----------|-----------|
| Any broken behaviour was fixed | `bug` |
| Any new feature or improvement was added | `enhancement` |
| Changes touch the UI (dashboard, decorations, sidebar, icons, colors) | `ui` |
| CI, GitHub Actions, publish pipeline, version bump | `publish` |
| Docs only | `documentation` |

Examples of multi-label combinations (based on real PRs in this repo):
- Bug fix that also improves a feature → `bug` + `enhancement`
- Bug fix with visual changes → `bug` + `enhancement` + `ui`
- CI/release change → `publish`

To decide, read the commits and description — don't guess from type alone. A PR titled `[Fix]` can still get `enhancement` if it improves usability alongside fixing a bug.

Output the PR URL when done so the user can see it immediately.

## Branch naming reference (use when creating branches before PRs)

```
fix/short-kebab-description      ← bug fixes
feat/short-kebab-description     ← new features  
chore/short-kebab-description    ← tooling, CI, config
refactor/short-kebab-description ← code cleanup
docs/short-kebab-description     ← documentation
```

All lowercase. Hyphens only. Under 40 characters total. No ticket numbers in branch names.
