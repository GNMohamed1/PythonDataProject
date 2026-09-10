Here is a complete, production-ready `INSTRUCTIONS.md` file designed for your team. You can drop this directly into your repository root so everyone follows the exact same workflow from day one.

---

```markdown
# 🇪🇬 Egypt Smart Relocation Advisor — Team Onboarding & Contribution Guide

Welcome to the team! This document outlines our setup steps, development workflow, git standards, and repository structure. Following these instructions ensures everyone works in an identical environment and keeps our git history clean for portfolio and academic review.

---

## 📋 Prerequisites

Before starting, ensure you have the following installed on your machine:

1. **Git** ([Download Git](https://git-scm.com/))
2. **Python 3.10+**
3. **`uv` Package Manager** ([Installation Guide](https://github.com/astral-sh/uv))
   * **Windows (PowerShell):** `powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"`
   * **macOS / Linux:** `curl -LsSf https://astral.sh/uv/install.sh | sh`

---

## 🚀 1. Quickstart Setup (5 Minutes)

Run these commands in order from your terminal to set up your local development environment:

```bash
# 1. Clone the repository
git clone https://github.com/GNMohamed1/PythonDataProject.git
cd PythonDataProject

# 2. Synchronize dependencies using uv (creates .venv automatically)
uv sync

# 3. Create your local environment file
cp .env.example .env

# 4. Launch the Streamlit application
uv run streamlit run app.py

```

---

## 📁 2. Repository Layout

Place new code into the correct directory to keep the project modular:

```text
├── .env.example            # Template for environment variables (Committed)
├── .gitignore              # Ignores .venv, raw data, and credentials
├── INSTRUCTIONS.md         # Team guide (This file)
├── README.md               # Public project overview for portfolio
├── pyproject.toml          # Project configuration & dependencies
├── uv.lock                 # Fixed dependency lockfile (Committed)
│
├── data/                   # LOCAL ONLY (Git ignored)
│   ├── raw/                # Raw downloaded shapefiles/GeoJSONs
│   └── processed/          # Cleaned CSVs and merged data
│
├── scripts/                    # Python Modules & Business Logic
│   ├── __init__.py
│   ├── data_gather.py      # OSM, Overpass & Air Quality extractors
│   ├── imputation.py       # Random Forest bathroom prediction model
│   └── scoring.py          # Dynamic MCDA scoring engine
│
├── notebooks/              # Jupyter notebooks for data exploration
│   └── exploration.ipynb
│
└── app.py                  # Main Streamlit web frontend

```

---

## 📦 3. Managing Dependencies with `uv`

**NEVER use plain `pip install` directly.** Always use `uv` so dependencies are tracked in `pyproject.toml` and locked in `uv.lock`.

* **Adding a new library:**
```bash
uv add <package-name>
# Example: uv add scikit-learn

```


* **Removing a library:**
```bash
uv remove <package-name>

```


* **Updating dependencies after pulling teammate updates:**
```bash
uv sync

```



---

## 🌿 4. Git Hygiene & Branching Rules

### Rule #1: Never Commit directly to `master`

All work must happen on topic branches and be merged via Pull Requests (PRs).

### Branch Naming Conventions:

* `feat/<feature-name>` — New features (e.g., `feat/scoring-algorithm`, `feat/map-layer`)
* `fix/<bug-name>` — Bug fixes (e.g., `fix/geocoding-fallback`)
* `data/<pipeline-name>` — Data cleaning or fetching scripts (e.g., `data/impute-bathrooms`)
* `ui/<view-name>` — Streamlit UI updates (e.g., `ui/sidebar-filters`)

### Standard Workflow:

```bash
# 1. Make sure master is up to date
git checkout master
git pull origin master

# 2. Create your branch
git checkout -b feat/add-scoring-engine

# 3. Make changes and commit using Conventional Commits
git add .
git commit -m "feat: implement weighted MCDA algorithm for district scoring"

# 4. Push your branch
git push origin feat/add-scoring-engine

# 5. Open a Pull Request on GitHub and request a review from a teammate

```

---

## 💬 5. Commit Message Conventions

Use clear prefix tags in your commit messages so professors and recruiters can read our progress history:

| Tag | Usage | Example |
| --- | --- | --- |
| `feat:` | New feature or module | `feat: add Random Forest model for bathroom imputation` |
| `fix:` | Bug fix | `fix: resolve missing geometry error in Zamalek polygon` |
| `data:` | Pipeline or dataset processing | `data: update OSM tags for cafe and hospital extraction` |
| `ui:` | Streamlit layout / charts | `ui: add radar chart for district analytics` |
| `docs:` | Documentation changes | `docs: update INSTRUCTIONS.md with uv setup` |

---

## 🔒 6. Data & Secret Safety Rules

1. **Do NOT commit `.env` files or API keys.**
2. **Do NOT commit `.csv` or `.geojson` datasets.** Data scripts must generate these files dynamically inside the local `data/` folder.
3. If you add new environment variables, remember to add their blank placeholders to `.env.example`.
