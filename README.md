<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Hugo-0.161.1-FF4088?logo=hugo&logoColor=white" alt="Hugo">
  <img src="https://img.shields.io/badge/license-MIT-blue" alt="License">
  <img src="https://img.shields.io/badge/PRs-welcome-brightgreen" alt="PRs Welcome">
</p>

<h1 align="center">🐍 Complete Python Learning Path</h1>

<p align="center">
  <strong>From zero to production-ready — your one-stop resource to learn, revise, and ace Python interviews.</strong>
</p>

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
  <strong>Happy Learning! 🐍</strong><br>
  <sub>Built with ❤️ using Hugo and the Book theme</sub>
</p>
