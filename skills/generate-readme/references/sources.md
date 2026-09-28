# Web Search & Fetch Playbook

This file tells the skill exactly where to look for README inspiration. Read it before running any searches.

---

## Search Query Templates

Adapt these to the specific project language and type. Run 2–3 in parallel.

### Find top repos by language + type
```
top starred python cli tool github README site:github.com
top starred typescript vscode extension github open source
best rust library github README example
```

### Find curated lists
```
awesome-readme github.com examples
awesome python github README
best open source javascript project README template
```

### Find recent trending
```
github trending python this week
github trending typescript 2024
trending open source <language> projects github
```

### Find README guides / standards
```
"how to write a good README" github
opensource.guide README best practices
"make a readme" site:makeareadme.com
```

---

## Authoritative Sources to Fetch From

### Curated README galleries (fetch these directly)
- `https://raw.githubusercontent.com/matiassingers/awesome-readme/master/readme.md` — curated list of excellent READMEs
- `https://www.makeareadme.com/` — opinionated guide on structure
- `https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes`

### Well-known repos with excellent READMEs (fetch by project type)

**CLI tools:**
- `https://raw.githubusercontent.com/cli/cli/trunk/README.md` (GitHub CLI)
- `https://raw.githubusercontent.com/sharkdp/bat/master/README.md` (bat)
- `https://raw.githubusercontent.com/junegunn/fzf/master/README.md` (fzf)

**Python libraries:**
- `https://raw.githubusercontent.com/psf/requests/main/README.md`
- `https://raw.githubusercontent.com/tiangolo/fastapi/master/README.md`
- `https://raw.githubusercontent.com/pydantic/pydantic/main/README.md`

**VS Code extensions (fetch the Marketplace page, not just raw README — Marketplace renders the README as the full listing):**
- CodeRabbit: `https://marketplace.visualstudio.com/items?itemName=CodeRabbit.coderabbit-vscode` — best example of hook-first + multiple GIFs throughout
- GitLens: `https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens` — best example of progressive disclosure, feature-per-image layout
- Error Lens: `https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens` — minimal but effective, single demo image early
- Draw.io: `https://raw.githubusercontent.com/hediet/vscode-drawio/master/README.md`
- Code Spell Checker: `https://raw.githubusercontent.com/streetsidesoftware/vscode-spell-checker/main/README.md`

**Key insight from top VS Code extension pages:**
The README.md IS the Marketplace listing. Always fetch the Marketplace URL (not raw GitHub) to see exactly what users see. The rendering differs — Marketplace strips HTML comments, renders relative image paths relative to the repo root.
For image paths to work on the Marketplace, images must either be: (a) relative paths pointing to `assets/` in the repo root, or (b) absolute URLs. Relative paths work because vsce bundles the assets folder.

**TypeScript / Node libraries:**
- `https://raw.githubusercontent.com/sindresorhus/got/main/readme.md`
- `https://raw.githubusercontent.com/colinhacks/zod/master/README.md`

**Web apps:**
- `https://raw.githubusercontent.com/calcom/cal.com/main/README.md`
- `https://raw.githubusercontent.com/maybe-finance/maybe/main/README.md`

**Data science / ML:**
- `https://raw.githubusercontent.com/huggingface/transformers/main/README.md`
- `https://raw.githubusercontent.com/ultralytics/ultralytics/main/README.md`

---

## How to Fetch a Raw README

Pattern:
```
https://raw.githubusercontent.com/<owner>/<repo>/main/README.md
```

If that returns 404, try:
```
https://raw.githubusercontent.com/<owner>/<repo>/master/README.md
```

If the repo was found via a web search, extract the `<owner>/<repo>` from the GitHub URL.

---

## What to Extract from Each README

When you fetch a README, pull out:
1. **Section list** — H2 headings in order
2. **Opening pattern** — how the first 5 lines are structured
3. **Badge row** — which badges, in what order
4. **Code example format** — inline vs block, how much shown
5. **Length estimate** — roughly how many words

Use this to make your structural decision, not to copy content verbatim.

---

## Trending Repos (GitHub API)

To find what's trending right now, search:
```
github trending <language> today site:github.com
```
Or fetch:
```
https://github.com/trending/<language>?since=weekly
```
Pick repos with 100+ stars and a language that matches the user's project.
