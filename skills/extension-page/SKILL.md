---
name: extension-page
description: Write the VS Code Marketplace listing README.md for an extension. Use when the user wants to write, update, or publish their VS Code extension page. Developer docs go in DEV.md, not here.
allowed-tools: Bash Read Glob Grep WebFetch WebSearch Agent
argument-hint: [path to extension root, or "." for current directory]
---

# Write VS Code Extension Marketplace Page

README.md for a VS Code extension is rendered verbatim as the Marketplace listing. Write it entirely for end users. Zero developer content in this file.

**NEVER include:** badges, Contributing section, License section, project structure trees, npm/build/test commands, architecture explanations.

---

## Step 1 — Explore the Extension (Explore subagent)

Spawn an Explore subagent. This keeps codebase detail out of your context:

```
Agent({
  subagent_type: "Explore",
  description: "Explore VS Code extension codebase",
  prompt: "Explore the VS Code extension at [path or current directory]. Return ONLY:
  1. displayName, description, publisher from package.json
  2. All commands from contributes.commands (title + command id for each)
  3. All settings from contributes.configuration.properties (key, type, default, description for each)
  4. Contents of assets/ folder — list every file
  5. Current README.md H2 section headings (headings only, not content)
  6. Whether DEV.md exists
  Do not return raw file contents. Be concise."
})
```

---

## Step 2 — Research Marketplace Pages (Research subagent)

Spawn a research subagent to fetch reference pages without bringing raw HTML into this context:

```
Agent({
  description: "Research VS Code Marketplace page patterns",
  prompt: "Fetch 2 of these VS Code Marketplace pages (pick the most relevant to this extension's domain):
  - https://marketplace.visualstudio.com/items?itemName=CodeRabbit.coderabbit-vscode  (AI/code review tool)
  - https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens              (git/source control)
  - https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens         (code diagnostics/display)
  - https://marketplace.visualstudio.com/items?itemName=hediet.vscode-drawio         (visual/diagram tool)

  For each page, return ONLY these extracted patterns — no raw content:
  1. Hook structure: does it lead with problem or feature? How long is the opening?
  2. Badges: yes/no, which ones?
  3. Feature section: bold-headline+GIF vs bullet list vs prose?
  4. Section order: list the H2 headings in order
  5. Approximate word count
  6. Does it have Contributing or License sections in the body?

  End with: which 2 pages you fetched."
})
```

Tell the user which 2 pages were referenced.

---

## Step 3 — Plan (confirm before writing)

Show the user a short bullet list of planned README.md sections. Say:
> "Here's what I'm planning — let me know if you want to adjust anything, otherwise I'll go ahead."

---

## Step 4 — Write README.md

### Hard rules — no exceptions

- **No badges** — the Marketplace sidebar already shows version, installs, rating, license, publisher
- **No Contributing section** — goes in DEV.md
- **No License section** — shown in Marketplace sidebar automatically
- **No project structure** — developer content
- **No npm commands** — developer content

### Structure

```markdown
# [displayName]
> One outcome-focused tagline (not a feature list — what does the user GET?)

[Hook: 2–3 sentences. LEAD WITH THE PROBLEM. What frustration does this solve?
Do not start with "Coverage Visualizer is a..." — start with the user's situation.]

![Demo](assets/demo.gif)

---

## Features

**[Feature name]** — one sentence of concrete user benefit.

[GIF or screenshot immediately after its feature, if available]

[Repeat — bold headline + sentence + visual for each major feature]

---

## Supported Formats   (only if the extension handles multiple input formats)

| Format | How to generate |
|--------|----------------|
| ...    | ...            |

No [runtime] required — the extension reads all formats natively.

---

## Installation

Search for **[displayName]** in the Extensions panel (`Cmd+Shift+X` / `Ctrl+Shift+X`) and click Install.

---

## Quick Start

[2–4 numbered steps. Start from zero. End at the "wow" moment. Use code blocks.]

---

## Commands   (only if the extension contributes commands)

| Command | What it does |
|---------|-------------|
| ...     | ...          |

---

## Configuration

| Setting | Default | Description |
|---------|---------|-------------|
[one row per setting from contributes.configuration.properties]
```

### Asset rules

- If `assets/demo.gif` exists → `![Demo](assets/demo.gif)` — use the real path, no placeholder
- If per-feature GIFs exist (e.g. `assets/demo-highlights.gif`) → place each after its feature
- If no GIFs exist → `<!-- demo GIF: record [specific action to show] -->` as placeholder
- Paths must be relative — vsce bundles the `assets/` folder so relative paths work on the Marketplace

### Writing tone

- Active voice, imperative: "Run `pytest`" not "You can run..."
- Short sentences — this is a product page, not prose
- Every code snippet in a fenced block with language specified
- Target: 300–500 words. Dense with visuals, light on text.

---

## Step 5 — Write DEV.md (if it doesn't exist)

If DEV.md does not exist, offer to create it. DEV.md must contain everything a contributor needs:
- Prerequisites (Node version, VS Code version, npm)
- Clone + install steps
- How to launch the dev host (F5 in VS Code)
- Architecture overview (what each src/ file/folder does)
- All npm commands (compile, watch, test, lint, test:coverage)
- Project structure tree
- How to run a single test
- Fixture regeneration instructions (if applicable)
- PR guidelines (branch naming, test requirements, PR description format)

---

## Step 6 — Deliver

1. Write `README.md` to the extension root
2. Write `DEV.md` if it was missing and user agreed
3. Report:
   - Which 2 Marketplace pages were referenced
   - Each GIF placeholder left and exactly what to record
   - Whether DEV.md was written or already existed
