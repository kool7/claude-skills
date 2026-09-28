---
name: generate-readme
description: Generate a full, industry-standard README.md for non-extension GitHub projects (libraries, CLIs, web apps, APIs, data science). Includes Installation, Contributing, License, and badges. For VS Code extensions, use /extension-page or /readme instead. Use when the user asks to create or improve a README for a non-extension project.
allowed-tools: Bash Read Glob Grep WebSearch WebFetch Agent
argument-hint: [path to project, or "." for current directory]
---

# Generate README

Produce a polished, industry-standard `README.md` grounded in what you find in the codebase and real-world examples from top GitHub projects.

**If the project is a VS Code extension** (package.json contains `"engines": { "vscode": ... }`): stop immediately and tell the user to use `/extension-page` or `/readme` instead. This skill is for non-extension projects only.

Never produce a generic template. Every section must be grounded in what you actually found.

---

## Step 1 — Explore the Project (Explore subagent)

Spawn an Explore subagent to keep codebase details out of your context:

```
Agent({
  subagent_type: "Explore",
  description: "Explore project for README generation",
  prompt: "Explore this project at [path]. Return ONLY these facts — no file contents:
  1. Project type: CLI tool / Python library / web app / API / data science / other
  2. Primary language and framework
  3. What the project does in 1–2 plain sentences
  4. Install command (from package.json scripts, pyproject.toml, Makefile, setup.py)
  5. Test command (from scripts)
  6. License type (from LICENSE file or package.json license field)
  7. Current README.md H2 headings if README exists (headings only)
  8. Whether CI config exists (.github/workflows/, .travis.yml, Dockerfile)
  9. Whether .env.example exists and any key variable names
  Be concise."
})
```

---

## Step 2 — Research Top GitHub READMEs (Research subagent)

Spawn a research subagent to fetch examples without polluting this context:

```
Agent({
  description: "Research top GitHub READMEs for structural patterns",
  prompt: "Find and fetch 2–3 README files from top starred GitHub repos of the same type as this project.

  Run these web searches first (adapt to the actual project type and language):
  - 'top starred [language] [project-type] github site:github.com'
  - 'awesome [project-type] github README examples'

  Then fetch raw READMEs from the most relevant repos:
  https://raw.githubusercontent.com/<owner>/<repo>/main/README.md
  (try master if main fails)

  Also check these curated sources relevant to the project type:
  - Python libraries: requests, fastapi, pydantic READMEs
  - CLI tools: cli/cli, sharkdp/bat, junegunn/fzf READMEs
  - TypeScript/Node: sindresorhus/got, colinhacks/zod READMEs
  - Web apps: calcom/cal.com, maybe-finance/maybe READMEs
  - Data/ML: huggingface/transformers, ultralytics/ultralytics READMEs

  For each README fetched, return ONLY extracted patterns — no raw content:
  1. Section order (H2 headings in order)
  2. Opening pattern: one-liner tagline / paragraph / badges-first
  3. Badge style: none / compact row / verbose
  4. Code example format: how much shown, inline vs block
  5. Approximate word count

  End with: repo name and URL for each one you fetched."
})
```

Tell the user which repos were referenced before writing.

---

## Step 3 — Pick Structure

Based on the project type from Step 1, apply the matching section order. Real-world patterns from Step 2 beat these defaults when they conflict.

| Project type | Section order |
|---|---|
| Python library | H1 + tagline, badges (PyPI/Python/License/CI), overview, Features, Installation (`pip install`), Quick Start with code example, Usage, Development, Contributing, License |
| CLI tool | H1 + tagline, badges (Version/License/CI), overview, Installation (all package managers that apply), Usage with flags table + examples, Configuration, Contributing, License |
| Web app / frontend | H1 + tagline, badges (CI/License), overview, Features, Tech Stack, Getting Started (prerequisites + commands), Environment Variables, Testing, Deployment, Contributing, License |
| API / backend | H1 + tagline, badges (CI/Docker/License), overview, Features, Getting Started (prerequisites + Docker option), API Reference (key endpoints table), Configuration, Testing, Contributing, License |
| Data science / ML | H1 + tagline, badges (Python/License), overview, Results (key metric upfront), Dataset, Setup, Usage (Training + Inference sections), Project Structure, Contributing, License |

Show the user the planned section list as a short bullet list:
> "Here's what I'm planning — let me know if you want to adjust anything, otherwise I'll go ahead."

---

## Step 4 — Write README.md

### Always include

**H1 project name** + single punchy tagline on the line below (npm-style, not a sentence)

**Badges** — only include badges that genuinely apply. Common picks:
- CI status (GitHub Actions / Travis CI)
- Version (npm / PyPI / crates.io) — only if published
- License
- Language / platform version

**Overview** — 2–4 sentences. What it does, who it's for, why it exists. No buzzwords.

**Features** — 4–8 bullet points, concrete and specific ("Groups consecutive coverage lines into ranges" not "Easy to use")

**Installation** — exact commands copy-pasted from actual project config

**Quick Start / Usage** — at least one real working example with input and expected output

**Contributing** — 3–5 lines: fork, feature branch, PR. Reference CONTRIBUTING.md if it exists.

**License** — one line with type and link to LICENSE file

### Include when genuinely relevant

- **Screenshots / Demo** — `<!-- Add screenshot here -->` placeholder if visual but no image
- **Configuration** — if the project has env vars, config files, or CLI flags
- **Running Tests** — exact test command
- **Project Structure** — for non-obvious layouts (monorepos, plugins)
- **Roadmap / Limitations** — only if there's real content
- **Acknowledgements** — if the project is built on notable tools

### Writing rules

- Active voice, imperative: "Run `npm install`" not "You can run..."
- Short sentences — documentation not prose
- Every command/code in a fenced block with language specified
- No filler — if a section has nothing real to say, leave it out
- Target: 300–600 words for small/medium projects; up to 900 for larger ones

---

## Step 5 — Deliver

1. Write `README.md` to the project root
2. Tell the user:
   - Which repos you drew inspiration from (name + URL)
   - Any non-obvious structural choices
   - Any sections you omitted and why
3. Offer the most relevant follow-up: "Want me to also generate a `CONTRIBUTING.md`?" or "Should I add a GitHub Actions CI workflow?"
