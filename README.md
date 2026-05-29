<p align="center">
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1250 400" width="100%" style="max-width:1250px;display:block;margin:0 auto;border-radius:12px">
    <defs>
      <linearGradient id="bgGradPy" x1="0%" y1="0%" x2="100%" y2="100%">
        <stop offset="0%" stop-color="#0a1628"><animate attributeName="stop-color" values="#0a1628;#1a1a2e;#0f3460;#0a1628" dur="10s" repeatCount="indefinite"/></stop>
        <stop offset="50%" stop-color="#16213e"><animate attributeName="stop-color" values="#16213e;#0f3460;#1a1a2e;#16213e" dur="10s" repeatCount="indefinite"/></stop>
        <stop offset="100%" stop-color="#1a1a2e"><animate attributeName="stop-color" values="#1a1a2e;#0a1628;#16213e;#1a1a2e" dur="10s" repeatCount="indefinite"/></stop>
      </linearGradient>
      <linearGradient id="pyBlue" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" stop-color="#306998"/><stop offset="100%" stop-color="#1c4c7c"/></linearGradient>
      <linearGradient id="pyYellow" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" stop-color="#FFD43B"/><stop offset="100%" stop-color="#f5b700"/></linearGradient>
      <filter id="glowPy"><feGaussianBlur stdDeviation="3" result="blur"/><feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge></filter>
      <pattern id="gridPy" width="40" height="40" patternUnits="userSpaceOnUse"><path d="M 40 0 L 0 0 0 40" fill="none" stroke="#ffffff" stroke-width="0.5" opacity="0.03"/></pattern>
    </defs>
    <rect width="1250" height="400" fill="url(#bgGradPy)"/><rect width="1250" height="400" fill="url(#gridPy)"/>
    <!-- Python Logo -->
    <g transform="translate(50, 70)">
      <path d="M 60,0 C 27,0 0,27 0,60 L 0,100 C 0,115 12,125 27,125 L 45,125 C 60,125 72,115 72,100 L 72,90 C 72,80 64,72 54,72 L 18,72 L 18,64 C 18,54 26,46 36,46 L 60,46 L 72,46 L 72,28 C 72,13 60,0 45,0 Z" fill="url(#pyBlue)"><animate attributeName="opacity" values="0.9;1;0.9" dur="3s" repeatCount="indefinite"/></path>
      <path d="M 60,125 C 93,125 120,98 120,65 L 120,25 C 120,10 108,0 93,0 L 75,0 C 60,0 48,10 48,25 L 48,35 C 48,45 56,53 66,53 L 102,53 L 102,61 C 102,71 94,79 84,79 L 60,79 L 48,79 L 48,97 C 48,112 60,125 75,125 Z" fill="url(#pyYellow)"><animate attributeName="opacity" values="1;0.9;1" dur="3s" repeatCount="indefinite"/></path>
    </g>
    <!-- Left content group -->
    <g filter="url(#glowPy)">
      <text x="190" y="110" font-family="'Segoe UI',Arial,sans-serif" font-size="46" font-weight="800" fill="#fff">
        <tspan fill="#FFD43B">Python</tspan><tspan fill="#fff"> Learning Path</tspan>
        <animate attributeName="opacity" values="0;1" dur="1.5s" fill="freeze"/>
      </text>
    </g>
    <text x="190" y="152" font-family="'Segoe UI',Arial,sans-serif" font-size="19" fill="#8892b0" opacity="0">
      <tspan>From zero to production-ready — learn, revise,</tspan>
      <animate attributeName="opacity" values="0;1" dur="2s" begin="0.8s" fill="freeze"/>
    </text>
    <text x="190" y="178" font-family="'Segoe UI',Arial,sans-serif" font-size="19" fill="#e06c75" opacity="0" font-style="italic">
      <tspan>and ace your interview 🎯</tspan>
      <animate attributeName="opacity" values="0;1" dur="2s" begin="1.2s" fill="freeze"/>
    </text>
    <!-- Badges -->
    <g transform="translate(190, 215)" opacity="0">
      <animate attributeName="opacity" values="0;1" dur="1s" begin="1.8s" fill="freeze"/>
      <rect x="0" y="0" width="95" height="28" rx="14" fill="#306998"/><text x="47" y="19" font-family="Arial,sans-serif" font-size="13" font-weight="600" fill="#fff" text-anchor="middle">18 Chapters</text>
      <rect x="105" y="0" width="95" height="28" rx="14" fill="#6cc644"/><text x="152" y="19" font-family="Arial,sans-serif" font-size="13" font-weight="600" fill="#fff" text-anchor="middle">6 Practice Tests</text>
      <rect x="210" y="0" width="100" height="28" rx="14" fill="#e06c75"/><text x="260" y="19" font-family="Arial,sans-serif" font-size="13" font-weight="600" fill="#fff" text-anchor="middle">50+ Q&A</text>
      <rect x="320" y="0" width="95" height="28" rx="14" fill="#61afef"/><text x="367" y="19" font-family="Arial,sans-serif" font-size="13" font-weight="600" fill="#fff" text-anchor="middle">Open Source</text>
    </g>
    <!-- Code window -->
    <g transform="translate(820, 55)" opacity="0">
      <animate attributeName="opacity" values="0;1" dur="1.5s" begin="1s" fill="freeze"/>
      <rect x="0" y="0" width="380" height="250" rx="10" fill="#1e293b" stroke="#334155" stroke-width="1.5"/>
      <rect x="0" y="0" width="380" height="35" rx="10" fill="#0f172a"/><rect x="0" y="25" width="380" height="10" fill="#0f172a"/>
      <circle cx="20" cy="17" r="6" fill="#ff5f56"/><circle cx="40" cy="17" r="6" fill="#ffbd2e"/><circle cx="60" cy="17" r="6" fill="#27c93f"/>
      <text x="190" y="22" font-family="monospace" font-size="12" fill="#8892b0" text-anchor="middle">main.py</text>
      <!-- Line 1 -->
      <text x="15" y="60" font-family="monospace" font-size="12"><tspan fill="#4a5568"> 1  </tspan><tspan fill="#6cc644"># Python Learning Path</tspan></text>
      <!-- Line 2 -->
      <text x="15" y="78" font-family="monospace" font-size="12"><tspan fill="#4a5568"> 2  </tspan><tspan fill="#6cc644"># Master the fundamentals 🐍</tspan></text>
      <!-- Line 3 -->
      <text x="15" y="100" font-family="monospace" font-size="12"><tspan fill="#4a5568"> 3  </tspan><tspan fill="#61afef">import</tspan><tspan fill="#e5c07b"> math</tspan></text>
      <!-- Line 4 -->
      <text x="15" y="118" font-family="monospace" font-size="12"><tspan fill="#4a5568"> 4  </tspan><tspan fill="#61afef">from</tspan><tspan fill="#e5c07b"> typing</tspan><tspan fill="#61afef"> import</tspan><tspan fill="#e5c07b"> List</tspan></text>
      <!-- Line 5 -->
      <text x="15" y="136" font-family="monospace" font-size="12"><tspan fill="#4a5568"> 5  </tspan></text>
      <!-- Line 6 -->
      <text x="15" y="156" font-family="monospace" font-size="12"><tspan fill="#4a5568"> 6  </tspan><tspan fill="#61afef">class</tspan><tspan fill="#e5c07b"> Student</tspan><tspan fill="#abb2bf">:</tspan></text>
      <!-- Line 7 -->
      <text x="15" y="174" font-family="monospace" font-size="12"><tspan fill="#4a5568"> 7  </tspan><tspan fill="#61afef">    def</tspan><tspan fill="#e06c75"> __init__</tspan><tspan fill="#abb2bf">(self, name: </tspan><tspan fill="#e5c07b">str</tspan><tspan fill="#abb2bf">):</tspan></text>
      <!-- Line 8 -->
      <text x="15" y="192" font-family="monospace" font-size="12"><tspan fill="#4a5568"> 8  </tspan><tspan fill="#61afef">        self</tspan><tspan fill="#abb2bf">.name = name</tspan></text>
      <!-- Line 9 -->
      <text x="15" y="214" font-family="monospace" font-size="12"><tspan fill="#4a5568"> 9  </tspan></text>
      <!-- Line 10 -->
      <text x="15" y="232" font-family="monospace" font-size="12"><tspan fill="#4a5568">10  </tspan><tspan fill="#61afef">def</tspan><tspan fill="#e06c75"> calc_avg</tspan><tspan fill="#abb2bf">(grades: </tspan><tspan fill="#e5c07b">List[float]</tspan><tspan fill="#abb2bf">) -> </tspan><tspan fill="#e5c07b">float</tspan><tspan fill="#abb2bf">:</tspan></text>
      <!-- Blinking cursor at end of line 10 -->
      <rect x="348" y="226" width="7" height="14" fill="#FFD43B" opacity="0"><animate attributeName="opacity" values="0;1;0" dur="1s" repeatCount="indefinite"/></rect>
    </g>
  </svg>
</p>

<p align="center">
  <a href="https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white"><img src="https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white" alt="Python"></a>
  <a href="https://img.shields.io/badge/Hugo-0.161.1-FF4088?logo=hugo&logoColor=white"><img src="https://img.shields.io/badge/Hugo-0.161.1-FF4088?logo=hugo&logoColor=white" alt="Hugo"></a>
  <a href="https://img.shields.io/badge/license-MIT-blue"><img src="https://img.shields.io/badge/license-MIT-blue" alt="License"></a>
  <a href="https://img.shields.io/badge/PRs-welcome-brightgreen"><img src="https://img.shields.io/badge/PRs-welcome-brightgreen" alt="PRs Welcome"></a>
  <a href="https://github.com/prakashkuvvam/complete_python_notes/actions"><img src="https://img.shields.io/github/actions/workflow/status/prakashkuvvam/complete_python_notes/hugo-deploy.yml?label=deploy&logo=github" alt="Deploy Status"></a>
</p>

---

## 📖 Table of Contents

<p align="center">
  <a href="#-curriculum">Curriculum</a> •
  <a href="#-features">Features</a> •
  <a href="#-quick-start">Quick Start</a> •
  <a href="#-deployment">Deployment</a> •
  <a href="#-project-structure">Structure</a> •
  <a href="#-usage">Usage</a>
</p>

---

## 📚 Curriculum

This guide covers **18 comprehensive chapters** + **6 full-length practice tests**, organized into 4 progressive phases:

### 🏗️ Phase 1: Foundation

| # | Chapter | Topics |
|---|---------|--------|
| 01 | Introduction to Python & Setup | Installation, IDEs, virtual environments, pip, first script |
| 02 | Variables, Data Types & Operators | int, float, str, bool, type conversion, operators, type hints |
| 03 | Control Flow — Conditionals & Loops | if/elif/else, for/while, break/continue, match statement, comprehensions |
| 04 | Functions & Modules | def, parameters, scope, lambda, modules, packages, docstrings |

### 💪 Phase 2: Core Skills

| # | Chapter | Topics |
|---|---------|--------|
| 05 | Data Structures | Lists, tuples, sets, dictionaries, slicing, unpacking, comprehensions |
| 06 | Strings & String Manipulation | Methods, f-strings, regex, Unicode, encoding, formatting |
| 07 | File I/O & Exception Handling | open/close, context managers, try/except, custom exceptions, CSV/JSON |
| 08 | Object-Oriented Programming | Classes, inheritance, polymorphism, dunder methods, dataclasses, properties |

### 🚀 Phase 3: Advanced

| # | Chapter | Topics |
|---|---------|--------|
| 09 | Decorators, Generators & Context Managers | Closures, @decorator, yield, __enter__/__exit__, functools |
| 10 | Python Standard Library | math, datetime, collections, itertools, re, json, csv, hashlib |
| 11 | Testing with Python | unittest, pytest, mocking, TDD, coverage, doctests |
| 12 | APIs & Web Scraping | requests, BeautifulSoup, httpx, rate limiting, pagination |

### 🎯 Phase 4: Production & Interview Prep

| # | Chapter | Topics |
|---|---------|--------|
| 13 | Database & SQL Integration | SQLite, PostgreSQL, SQLAlchemy, Alembic, MongoDB |
| 14 | Concurrency, Async & Multiprocessing | Threading, asyncio, multiprocessing, GIL, concurrent.futures |
| 15 | Web Development with Flask & FastAPI | REST APIs, Pydantic, middleware, deployment |
| 16 | Data Science & Visualization | NumPy, Pandas, Matplotlib, Seaborn |
| 17 | Interview Questions & Answers | 50+ categorized Q&A with detailed explanations |
| 18 | Real-World Scenarios & Coding Problems | Log analyzer, ETL pipeline, rate limiter, chat server, and more |

### 📝 Practice Tests

| Test | Questions | Focus Area |
|------|-----------|------------|
| Practice Test 1 | 25 | Python Fundamentals |
| Practice Test 2 | 25 | Data Structures & Functions |
| Practice Test 3 | 25 | OOP & Exception Handling |
| Practice Test 4 | 25 | Advanced Python |
| Practice Test 5 | 25 | APIs, Databases & Web |
| Practice Test 6 | 30 | Full Mock Interview Assessment |

---

## ✨ Features

- ✅ **18 in-depth chapters** covering the complete Python ecosystem
- ✅ **6 interactive practice tests** with timers, instant scoring, and domain breakdowns
- ✅ **50+ interview questions** with detailed answers and code examples
- ✅ **Real-world coding scenarios** — log analyzers, ETL pipelines, rate limiters, and more
- ✅ **Interactive exam mode** — select answers, submit, and get instant feedback
- ✅ **Progress dashboard** — track your completion across all chapters and tests
- ✅ **Built-in exam timer** with start/pause controls and warning alerts
- ✅ **Dark theme** — easy on the eyes for extended study sessions
- ✅ **Code copy buttons** — one-click copy for all code examples
- ✅ **Search** — full-text search across all chapters
- ✅ **Mobile-responsive** — works on desktop, tablet, and phone
- ✅ **Sidebar & ToC collapse** — focus on what matters
- ✅ **KaTeX math rendering** — for technical content
- ✅ **GitHub Pages ready** — one-click deploy via GitHub Actions

---

## ✅ Prerequisites

- **Git** — to clone the repository
- **Python 3.10+** (optional) — to run the code examples yourself
- **Hugo Extended v0.161.1+** — to build and serve the site locally

---

## 🚀 Quick Start

### Local Development

```bash
# 1. Clone the repository
git clone https://github.com/prakashkuvvam/complete_python_notes.git
cd complete_python_notes

# 2. Initialize the theme submodule
git submodule update --init --recursive

# 3. Install Hugo (if not already installed)
# macOS:
brew install hugo

# Linux:
wget -O /tmp/hugo.deb https://github.com/gohugoio/hugo/releases/download/v0.161.1/hugo_extended_0.161.1_linux-amd64.deb
sudo dpkg -i /tmp/hugo.deb

# Windows (with scoop):
scoop install hugo-extended

# 4. Start the development server
hugo server -D
```

Open **http://localhost:1313/complete_python_notes/** in your browser.

### Building for Production

```bash
hugo --minify
```

The output will be in the `public/` directory.

---

## 🚀 Deployment

### Deploy to GitHub Pages (Automatic)

This repository includes a **GitHub Actions workflow** (`.github/workflows/hugo-deploy.yml`) that automatically builds and deploys the site to GitHub Pages on every push to `main` or `master`.

**Setup steps:**

1. Push the repository to GitHub
2. Go to **Settings > Pages**
3. Under **Source**, select **GitHub Actions**
4. The workflow will run automatically on the next push

The workflow will:
- ✅ Install Hugo 0.161.1 (extended)
- ✅ Checkout the repo with theme submodules
- ✅ Build the site with `--minify` and production base URL
- ✅ Upload the `public/` folder as a Pages artifact
- ✅ Deploy to GitHub Pages

### Manual Deploy (Any Static Host)

```bash
hugo --minify
# Upload the public/ directory to any static host:
# - Netlify
# - Vercel
# - AWS S3 + CloudFront
# - Any web server
```

---

## 📁 Project Structure

```
complete_python_notes/
├── content/
│   ├── _index.md                  # Home page
│   └── docs/
│       ├── _index.md              # Docs landing page
│       ├── 01-introduction-to-python-and-setup.md
│       ├── 02-python-basics-variables-data-types-operators.md
│       ├── ...                    # Chapters 3-24
│       ├── 25-progress-dashboard.md
│       └── 26-start-here.md
├── assets/
│   ├── banner.svg                 # Animated README banner
│   ├── _custom.scss               # Custom dark theme & exam styles
│   ├── copy-button.js             # Code block copy functionality
│   ├── exam-timer.js              # Exam countdown timer
│   └── exam-interactive.js        # Interactive quiz engine
├── layouts/
│   └── baseof.html                # Main layout template
├── themes/
│   └── book/                      # Hugo Book theme (git submodule)
├── static/
│   └── .nojekyll                  # GitHub Pages compatibility
├── archetypes/
│   └── default.md                 # Content archetype
├── .github/
│   └── workflows/
│       └── hugo-deploy.yml        # GitHub Actions deployment
├── hugo.toml                      # Hugo configuration
├── .gitmodules                    # Theme submodule reference
├── .gitignore
└── README.md
```

---

## 🎯 How to Use

### For Learners

1. **Start here** → Open `26-start-here.md` for a guided 4-week study plan
2. **Track progress** → Use the Progress Dashboard to mark chapters complete
3. **Read sequentially** → Chapters build on each other from 1 to 18
4. **Practice** → Take the interactive practice tests at the end of each phase
5. **Interview prep** → Use Ch 17 (Q&A) and Ch 18 (Scenarios) for focused preparation

### For Contributors

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-addition`)
3. Commit your changes (`git commit -m 'Add amazing addition'`)
4. Push to the branch (`git push origin feature/amazing-addition`)
5. Open a Pull Request

### Adding New Content

Each chapter is a Markdown file with Hugo front matter:

```markdown
---
title: "Ch N: Chapter Title"
weight: N
---

# Chapter Title

## Learning Objectives

...

## Content sections with code blocks

    ```python
    print("Hello, World!")
    ```

## 📝 Practice Problems

...

---
```

---

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| [Hugo](https://gohugo.io/) | Static site generator |
| [Hugo Book Theme](https://github.com/alex-shpak/hugo-book) | Documentation theme |
| [KaTeX](https://katex.org/) | Math rendering |
| SCSS | Custom styling & dark theme |
| Vanilla JS | Interactive exams, timers, dashboard |
| GitHub Actions | CI/CD & deployment |

---

## 📄 License

This project is provided for **educational purposes** under the MIT License. Feel free to use, modify, and share.

See the [LICENSE](LICENSE) file for details.

---

<p align="center">
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 900 180" width="100%" style="max-width:900px;display:block;margin:0 auto;border-radius:12px">
    <defs>
      <linearGradient id="ftGrad" x1="0%" y1="0%" x2="100%" y2="100%">
        <stop offset="0%" stop-color="#0a1628"><animate attributeName="stop-color" values="#0a1628;#1a1a2e;#0f3460;#0a1628" dur="8s" repeatCount="indefinite"/></stop>
        <stop offset="50%" stop-color="#16213e"><animate attributeName="stop-color" values="#16213e;#0f3460;#1a1a2e;#16213e" dur="8s" repeatCount="indefinite"/></stop>
        <stop offset="100%" stop-color="#1a1a2e"><animate attributeName="stop-color" values="#1a1a2e;#0a1628;#16213e;#1a1a2e" dur="8s" repeatCount="indefinite"/></stop>
      </linearGradient>
      <filter id="ftGlow"><feGaussianBlur stdDeviation="2.5" result="blur"/><feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge></filter>
      <pattern id="ftGrid" width="25" height="25" patternUnits="userSpaceOnUse"><path d="M 25 0 L 0 0 0 25" fill="none" stroke="#fff" stroke-width="0.4" opacity="0.04"/></pattern>
    </defs>
    <rect width="900" height="180" fill="url(#ftGrad)" rx="12"/>
    <rect width="900" height="180" fill="url(#ftGrid)" rx="12"/>
    <!-- Left accent bar -->
    <rect x="0" y="40" width="4" height="100" rx="2" fill="#FFD43B" opacity="0">
      <animate attributeName="opacity" values="0;0.8;0" dur="5s" begin="1s" repeatCount="indefinite"/>
    </rect>
    <!-- Python mini logo (enlarged) -->
    <g transform="translate(50, 55)" filter="url(#ftGlow)">
      <animateTransform attributeName="transform" type="translate" values="50,55;50,50;50,55" dur="4s" repeatCount="indefinite"/>
      <path d="M 25,0 C 11,0 0,11 0,25 L 0,42 C 0,48 5,52 11,52 L 19,52 C 25,52 30,48 30,42 L 30,37 C 30,33 27,30 22,30 L 8,30 L 8,27 C 8,22 11,19 16,19 L 25,19 L 30,19 L 30,12 C 30,5 25,0 19,0 Z" fill="#306998"/>
      <path d="M 25,52 C 39,52 50,41 50,27 L 50,10 C 50,4 45,0 39,0 L 31,0 C 25,0 20,4 20,10 L 20,15 C 20,19 23,22 28,22 L 42,22 L 42,25 C 42,30 39,33 35,33 L 25,33 L 20,33 L 20,40 C 20,48 25,52 31,52 Z" fill="#FFD43B"/>
    </g>
    <!-- Section: Title + Subtitle -->
    <g filter="url(#ftGlow)">
      <text x="100" y="70" font-family="'Segoe UI',Arial,sans-serif" font-size="28" font-weight="700" fill="#fff">
        🐍 Happy Learning!
        <animate attributeName="opacity" values="0;1" dur="1.5s" fill="freeze"/>
      </text>
    </g>
    <text x="100" y="100" font-family="'Segoe UI',Arial,sans-serif" font-size="15" fill="#8892b0">
      Built with ❤️ using Hugo &amp; the Book theme
      <animate attributeName="opacity" values="0;1" dur="2s" begin="0.5s" fill="freeze"/>
    </text>
    <!-- Links row -->
    <g opacity="0">
      <animate attributeName="opacity" values="0;1" dur="1s" begin="1.2s" fill="freeze"/>
      <a href="https://github.com/prakashkuvvam/complete_python_notes">
        <rect x="100" y="116" width="85" height="28" rx="14" fill="#1e293b" stroke="#3b82f6" stroke-width="1"/>
        <text x="142" y="135" font-family="Arial,sans-serif" font-size="13" fill="#3b82f6" text-anchor="middle" font-weight="600">⭐ Star</text>
      </a>
      <a href="https://github.com/prakashkuvvam/complete_python_notes/issues">
        <rect x="193" y="116" width="85" height="28" rx="14" fill="#1e293b" stroke="#e06c75" stroke-width="1"/>
        <text x="235" y="135" font-family="Arial,sans-serif" font-size="13" fill="#e06c75" text-anchor="middle" font-weight="600">📝 Issues</text>
      </a>
      <a href="https://github.com/prakashkuvvam/complete_python_notes/fork">
        <rect x="286" y="116" width="85" height="28" rx="14" fill="#1e293b" stroke="#6cc644" stroke-width="1"/>
        <text x="328" y="135" font-family="Arial,sans-serif" font-size="13" fill="#6cc644" text-anchor="middle" font-weight="600">🍴 Fork</text>
      </a>
    </g>
    <!-- Right side: Terminal (enlarged, repositioned) -->
    <g transform="translate(570, 35)" opacity="0">
      <animate attributeName="opacity" values="0;1" dur="1.5s" begin="0.8s" fill="freeze"/>
      <rect x="0" y="0" width="280" height="110" rx="8" fill="#1e293b" stroke="#334155" stroke-width="1.2"/>
      <rect x="0" y="0" width="280" height="26" rx="8" fill="#0f172a"/>
      <rect x="0" y="20" width="280" height="6" fill="#0f172a"/>
      <circle cx="14" cy="13" r="4.5" fill="#ff5f56"/><circle cx="30" cy="13" r="4.5" fill="#ffbd2e"/><circle cx="46" cy="13" r="4.5" fill="#27c93f"/>
      <text x="140" y="17" font-family="monospace" font-size="11" fill="#8892b0" text-anchor="middle">bash</text>
      <text x="12" y="50" font-family="monospace" font-size="13" fill="#6cc644">$</text>
      <text x="28" y="50" font-family="monospace" font-size="13" fill="#abb2bf">git clone &amp;&amp; hugo serve</text>
      <text x="12" y="72" font-family="monospace" font-size="13" fill="#abb2bf">Built 34 pages in 127 ms</text>
      <text x="12" y="94" font-family="monospace" font-size="13" fill="#6cc644">$</text>
      <text x="28" y="94" font-family="monospace" font-size="13" fill="#e5c07b">Ready to learn!</text>
      <rect x="130" y="86" width="7" height="14" fill="#FFD43B" opacity="0"><animate attributeName="opacity" values="0;1;0" dur="0.8s" repeatCount="indefinite"/></rect>
    </g>
    <!-- Bottom accent line -->
    <rect x="225" y="170" width="450" height="2" rx="1" fill="url(#pyBlue)" opacity="0">
      <animate attributeName="opacity" values="0;0.5;0" dur="3s" begin="2s" repeatCount="indefinite"/>
    </rect>
  </svg>
</p>
