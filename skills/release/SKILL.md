---
name: release
description: Bump the project version and push the release tag after merge. Use when the user wants to cut a release, bump a version, or tag a new version for publish.
allowed-tools: Bash Read
---

# Release

The version bump belongs in the feature PR — not a separate PR. This skill runs on your feature branch before raising the PR, so the version change ships with the code that warranted it.

## How it works

```
feature branch  →  npm version --no-git-tag-version  →  commit  →  PR  →  merge
main (after merge)  →  git tag v{X.Y.Z}  →  git push origin v{X.Y.Z}  →  publish triggered
```

Tag is pushed from main AFTER the PR merges. This is intentional — the tag points to a real commit on main, history stays clean, branch protection is respected.

---

## Step 1 — Detect stack and current version

Read `package.json` / `pyproject.toml` / `Cargo.toml` / `go.mod`. Check `CLAUDE.md` for a `release_command:` override.

| File | Stack | Bump command |
|------|-------|-------------|
| `package.json` | Node / npm | `npm version {type} --no-git-tag-version` |
| `pyproject.toml` (Poetry) | Python | `poetry version {type}` (no tag by default) |
| `pyproject.toml` (setuptools) | Python | edit `version =` manually |
| `Cargo.toml` | Rust | edit `version =` manually |
| `go.mod` | Go | no version file — skip to Step 4 |

Report the current version and stack.

## Step 2 — Determine bump type

If the user passed a type (e.g. `/release patch`), use it.

Otherwise read commits since last tag:
```
git log $(git describe --tags --abbrev=0)..HEAD --oneline
```

| What changed | Bump |
|--------------|------|
| Breaking change | `major` |
| New feature, no breaking change | `minor` |
| Bug fix or internal improvement | `patch` |

State the bump type and new version before doing anything. Wait for confirmation if unsure.

## Step 3 — Bump version on the current branch

```
npm version {patch|minor|major} --no-git-tag-version
```

`--no-git-tag-version` updates `package.json` only — no commit, no tag created yet. Then commit it:
```
git add package.json package-lock.json
git commit -m "bump: v{X.Y.Z}"
```

## Step 4 — Remind user of next steps

After the version is bumped and committed, output:

```
package.json bumped to v{X.Y.Z} and committed to this branch.

Include this in your PR — no separate PR needed.

After your PR is merged to main:
  git checkout main && git pull
  git tag v{X.Y.Z}
  git push origin v{X.Y.Z}

That tag push triggers GitHub Actions → Marketplace publish + GitHub Release.
```

If the user wants, offer to raise the PR now via `/create-pr`.

---

## Pushing the tag (after PR merge)

If the user runs `/release push` or says "push the tag":
```
git checkout main && git pull
git tag v{X.Y.Z}
git push origin v{X.Y.Z}
```

Report the Actions URL: `https://github.com/{owner}/{repo}/actions`
