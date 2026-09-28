# README Structures by Project Type

Pick the template that matches the project, then adapt based on real-world patterns found in Step 2 of the skill.

---

## VS Code Extension

**CRITICAL RULE FOR VS CODE EXTENSIONS:**
The README.md IS the Marketplace listing page. Every user who finds the extension on the VS Code Marketplace or the Marketplace website sees this file rendered. Write it entirely for end users — not developers, not contributors. No architecture diagrams, no test commands, no project structure trees in README.md. Those belong in CONTRIBUTING.md.

**What to put in README.md (Marketplace page):** hook, GIFs, features, install, quick start, config, license.
**What to put in CONTRIBUTING.md (developer docs):** architecture, project structure, how to run tests, how to add features, PR guidelines.

**GIF strategy (learned from CodeRabbit, GitLens, Error Lens):**
- Use multiple GIFs throughout, one per major feature group — not one big GIF at the top
- Place each GIF *after* the feature description it illustrates (show, don't tell)
- Each GIF should show ONE thing clearly (don't cram multiple features into one recording)
- Static screenshots are acceptable for simpler features; GIFs for anything with motion/workflow

**Asset conventions:**
- Check for an `assets/` folder in the project root before writing. If `assets/demo.gif` exists, use it as the main demo GIF immediately after the hook (no placeholder comment — use the real path).
- If `assets/` exists but specific feature GIFs don't, use `<!-- demo GIF: record X showing Y -->` placeholders for those slots.
- If `assets/` doesn't exist yet, use `<!-- Add assets/demo.gif here -->` style placeholders and note to the user they need to create the folder.
- Image paths must be relative (e.g., `assets/demo.gif`), not absolute. Relative paths work on the Marketplace because vsce bundles the assets folder.

```markdown
# Extension Name
> One-punchy-line tagline — outcome focused, not feature focused

[![CI](badge)](link) [![VS Code](badge)](link) [![License](badge)](link)

<!-- HOOK: 2-3 sentences. Lead with the PROBLEM, not the solution. -->
Your tests pass. But which lines did they actually hit? Coverage Visualizer shows you inline — green and red, right in the editor. No browser, no switching tabs, no mental mapping.

<!-- Demo GIF immediately after the hook — show the "wow" moment -->
![Coverage highlights in action](assets/demo-highlights.gif)

---

## Features

**Inline highlights** — green/red line backgrounds directly in the editor, with overview ruler markers so you can scan an entire file at a glance.

<!-- GIF: show highlights appearing after running show coverage command -->
![Inline highlights](assets/demo-feature-highlights.gif)

**CodeLens** — live coverage % above every `def` and `class` as you write.

<!-- GIF: show codelens above a function -->
![CodeLens coverage percentage](assets/demo-feature-codelens.gif)

**Dashboard** — interactive SVG ring chart, sortable file table, click-to-jump.

<!-- Screenshot: dashboard panel -->
![Dashboard](assets/demo-dashboard.png)

**Sidebar tree** — always-visible Coverage panel in the Explorer with pass/warn/fail icons per file.

**Hover tooltips** — hover any highlighted line for a ✓ Covered or ✗ Not covered message.

**Auto-reload** — file watchers detect changes to your coverage file and refresh instantly.

---

## Supported Formats

| Format | How to generate |
|---|---|
| `coverage.json` | `pytest --cov=. --cov-report=json` |
| `coverage.xml` | `pytest --cov=. --cov-report=xml` |
| `.coverage` | `pytest --cov=.` (raw SQLite) |

No Python runtime required — the extension reads all formats natively.

---

## Installation

Search for **Coverage Visualizer** in the Extensions panel (`Cmd+Shift+X` / `Ctrl+Shift+X`) and click Install.

Or install from VSIX:
```bash
code --install-extension coverage-visualizer-x.x.x.vsix
```

---

## Quick Start

```bash
# 1. Install pytest-cov in your Python project
pip install pytest-cov

# 2. Run your tests
pytest --cov=. --cov-report=json
```

Then open the Command Palette (`Cmd+Shift+P`) → **Coverage Visualizer: Show Coverage**.

Highlights appear on all open Python files immediately.

---

## Configuration

| Setting | Default | Description |
|---|---|---|
| `coverageVisualizer.thresholdGood` | `80` | % at or above which a file shows green |
| `coverageVisualizer.thresholdWarn` | `50` | % at or above which a file shows yellow |
| `coverageVisualizer.coveredHighlightColor` | `rgba(0,180,0,0.10)` | Background for covered lines |
| `coverageVisualizer.uncoveredHighlightColor` | `rgba(220,50,50,0.10)` | Background for uncovered lines |
| `coverageVisualizer.enableCodeLens` | `true` | Show coverage % above `def`/`class` |
| `coverageVisualizer.enableHoverMessages` | `true` | Covered/not-covered tooltip on hover |
| `coverageVisualizer.autoReloadOnChange` | `true` | Auto-reload when coverage files change |

---

## License
MIT — see [LICENSE](LICENSE)
```

**What NOT to include in README.md for VS Code extensions:**
- Project structure trees (`src/`, `tests/`, etc.) — goes in CONTRIBUTING.md
- `npm test` / `npm run compile` — developer commands, goes in CONTRIBUTING.md
- Architecture explanations — goes in CONTRIBUTING.md
- "How it works" with data flow diagrams — goes in CONTRIBUTING.md
- Contributing section (more than 1–2 lines pointing to CONTRIBUTING.md)

**CONTRIBUTING.md for VS Code extensions should have:**
- Prerequisites (Node version, VS Code, npm)
- Clone + install steps
- How to launch the dev host (F5 / Run Extension)
- Architecture overview (what each src/ file does)
- Test commands (`npm test`, `npx jest --testNamePattern "..."`)
- Project structure tree
- Branch naming conventions and PR guidelines
- How to add a new feature (which files to touch)

---

## Python Library / Package

```markdown
# library-name
> One-line tagline

![PyPI](badge) ![Python](badge) ![License](badge) ![CI](badge)

2–3 sentence overview.

## Features
- ...

## Installation
```bash
pip install library-name
```

## Quick Start
```python
from library_name import something

result = something.do_thing(input)
print(result)
```

## Usage
Explain the main API surface. Include function signatures and examples.

## Configuration
If applicable.

## Development
```bash
git clone https://github.com/user/library-name
cd library-name
pip install -e ".[dev]"
pytest
```

## Contributing
...

## License
MIT — see [LICENSE](LICENSE)
```

---

## CLI Tool

```markdown
# tool-name
> One-line tagline

![Version](badge) ![License](badge) ![CI](badge)

2–3 sentence overview of what it does from the command line.

## Installation

**Via npm:**
```bash
npm install -g tool-name
```

**Via pip:**
```bash
pip install tool-name
```

**From source:**
```bash
git clone ...
make install
```

## Usage
```bash
tool-name [options] <input>
```

### Options
| Flag | Description |
|---|---|
| `--flag` | What it does |

### Examples
```bash
# Example 1
tool-name input.txt --output result.json

# Example 2
tool-name --verbose --dry-run
```

## Configuration
Config file location and format, if applicable.

## Contributing
...

## License
...
```

---

## Web App / Frontend

```markdown
# App Name
> One-line tagline

![CI](badge) ![License](badge)

2–3 sentence overview.

## Features
- ...

## Tech Stack
- Framework: React / Vue / Svelte
- Styling: Tailwind / CSS Modules
- State: Zustand / Redux
- Backend: (if applicable)

## Getting Started

### Prerequisites
- Node.js 18+
- npm / yarn / pnpm

### Installation
```bash
git clone https://github.com/user/app-name
cd app-name
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

## Environment Variables
Create a `.env.local` file:
```
NEXT_PUBLIC_API_URL=https://...
DATABASE_URL=...
```

## Testing
```bash
npm test
npm run test:e2e
```

## Deployment
Brief notes on how to deploy (Vercel, Docker, etc.)

## Contributing
...

## License
...
```

---

## API / Backend Service

```markdown
# service-name
> One-line tagline

![CI](badge) ![Docker](badge) ![License](badge)

2–3 sentence overview.

## Features
- ...

## Getting Started

### Prerequisites
- Go 1.21+ / Node 18+ / Python 3.11+
- Docker (optional)

### Installation
```bash
git clone ...
cd service-name
cp .env.example .env
# Edit .env with your values
make run
```

### Docker
```bash
docker compose up
```

## API Reference
Brief overview of key endpoints, or link to generated docs (Swagger, etc.)

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/v1/items` | List items |
| POST | `/api/v1/items` | Create item |

## Configuration
Key env vars and what they control.

## Testing
```bash
make test
```

## Contributing
...

## License
...
```

---

## Data Science / ML Project

```markdown
# Project Name
> One-line tagline

![Python](badge) ![License](badge)

2–3 sentence overview of the problem being solved and approach taken.

## Results
Key metric or outcome upfront (accuracy, F1, benchmark score, etc.)

<!-- Add results chart or table here -->

## Dataset
Where data comes from, size, format, any licensing notes.

## Setup

```bash
git clone ...
cd project-name
pip install -r requirements.txt
```

## Usage

### Training
```bash
python train.py --config config/default.yaml
```

### Inference
```bash
python predict.py --input data/sample.csv --output results/
```

## Project Structure
```
├── data/           # Raw and processed data
├── notebooks/      # Exploratory analysis
├── src/            # Source code
├── models/         # Saved model weights
└── config/         # Configuration files
```

## Contributing
...

## License
...
```
