---
name: readme
description: Smart README skill — detects project type and applies the right rules. For VS Code extensions: writes README.md as a Marketplace product page (no badges/contributing/license) and DEV.md as the developer guide. For all other projects: writes a full README.md with installation, contributing, license, etc. Use this as the default entry point for any README task.
allowed-tools: Bash Read Glob Grep WebFetch WebSearch Agent
argument-hint: [path to project root, or "." for current directory]
---

# Smart README — Detect and Write

You are the entry point for all README generation. Detect what kind of project this is, then follow the matching rules below.

---

## Step 1 — Detect Project Type

Run these in parallel:
- `find $ARGUMENTS -maxdepth 3 -not -path '*/node_modules/*' -not -path '*/.git/*' -not -path '*/out/*' -not -path '*/dist/*'`
- Read `package.json` (or `pyproject.toml`, `Cargo.toml`, `go.mod` — whichever exists)

**Decision rule:**
- If `package.json` contains `"engines": { "vscode": ... }` → **VS Code Extension path** (see Section A below)
- Otherwise → **General Project path** (see Section B below)

Tell the user which path you're taking before proceeding.

---

## SECTION A — VS Code Extension

**Delegate entirely to the `extension-page` skill.** Tell the user:
> "This is a VS Code extension — running `/extension-page` rules."

Then invoke the `extension-page` skill with the same path argument. Do not re-implement its logic here.

---

## SECTION B — General Project

**Delegate entirely to the `generate-readme` skill.** Tell the user:
> "This is a general project — running `/generate-readme` rules."

Then invoke the `generate-readme` skill with the same path argument. Do not re-implement its logic here.
