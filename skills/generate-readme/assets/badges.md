# Badge Cheatsheet

Copy-paste shields.io badge markdown. Replace placeholders in `<>`.

Only include badges that genuinely apply to the project. A badge that links to nothing or shows "unknown" is worse than no badge.

---

## CI / Build Status

**GitHub Actions:**
```markdown
![CI](https://github.com/<owner>/<repo>/actions/workflows/<workflow-file>.yml/badge.svg)
```

**Travis CI:**
```markdown
[![Build Status](https://travis-ci.com/<owner>/<repo>.svg?branch=main)](https://travis-ci.com/<owner>/<repo>)
```

---

## Version / Release

**npm:**
```markdown
[![npm version](https://img.shields.io/npm/v/<package-name>.svg)](https://www.npmjs.com/package/<package-name>)
```

**PyPI:**
```markdown
[![PyPI version](https://img.shields.io/pypi/v/<package-name>.svg)](https://pypi.org/project/<package-name>/)
```

**VS Code Marketplace:**
```markdown
[![VS Code Marketplace](https://img.shields.io/visual-studio-marketplace/v/<publisher>.<extension-name>)](https://marketplace.visualstudio.com/items?itemName=<publisher>.<extension-name>)
```

**crates.io (Rust):**
```markdown
[![Crates.io](https://img.shields.io/crates/v/<crate-name>.svg)](https://crates.io/crates/<crate-name>)
```

**GitHub Release:**
```markdown
[![GitHub release](https://img.shields.io/github/v/release/<owner>/<repo>)](https://github.com/<owner>/<repo>/releases)
```

---

## License

```markdown
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
```

---

## Language / Runtime Version

**Python:**
```markdown
[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
```

**Node.js:**
```markdown
[![Node.js 18+](https://img.shields.io/badge/node-18+-green.svg)](https://nodejs.org/)
```

**TypeScript:**
```markdown
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-blue?logo=typescript)](https://www.typescriptlang.org/)
```

**VS Code Engine:**
```markdown
[![VS Code](https://img.shields.io/badge/VS%20Code-1.80+-blue?logo=visualstudiocode)](https://code.visualstudio.com/)
```

---

## Test Coverage

**Codecov:**
```markdown
[![codecov](https://codecov.io/gh/<owner>/<repo>/branch/main/graph/badge.svg)](https://codecov.io/gh/<owner>/<repo>)
```

**Coveralls:**
```markdown
[![Coverage Status](https://coveralls.io/repos/github/<owner>/<repo>/badge.svg?branch=main)](https://coveralls.io/github/<owner>/<repo>?branch=main)
```

---

## Downloads / Installs

**npm weekly downloads:**
```markdown
[![npm downloads](https://img.shields.io/npm/dw/<package-name>.svg)](https://www.npmjs.com/package/<package-name>)
```

**VS Code installs:**
```markdown
[![Installs](https://img.shields.io/visual-studio-marketplace/i/<publisher>.<extension-name>)](https://marketplace.visualstudio.com/items?itemName=<publisher>.<extension-name>)
```

---

## Repo Health

**GitHub stars:**
```markdown
[![GitHub Stars](https://img.shields.io/github/stars/<owner>/<repo>?style=social)](https://github.com/<owner>/<repo>/stargazers)
```

**Last commit:**
```markdown
[![Last Commit](https://img.shields.io/github/last-commit/<owner>/<repo>)](https://github.com/<owner>/<repo>/commits/main)
```

**Open issues:**
```markdown
[![Issues](https://img.shields.io/github/issues/<owner>/<repo>)](https://github.com/<owner>/<repo>/issues)
```

---

## Misc

**PRs Welcome:**
```markdown
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)
```

**Made with love:**
```markdown
[![Made with ❤️](https://img.shields.io/badge/Made%20with-%E2%9D%A4%EF%B8%8F-red.svg)]()
```

**Docker:**
```markdown
[![Docker Pulls](https://img.shields.io/docker/pulls/<owner>/<image>)](https://hub.docker.com/r/<owner>/<image>)
```

---

## Badge Arrangement Tips

- Put CI and version badges first (most useful at a glance)
- License badge near the end of the badge row
- Keep to 4–6 badges max — a wall of badges hurts readability
- Use consistent style: either all flat, all flat-square, or all default (don't mix)

Add `?style=flat-square` to any shields.io URL for the flat-square style:
```markdown
![CI](https://img.shields.io/badge/build-passing-brightgreen?style=flat-square)
```
