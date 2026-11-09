# Django Polls App — Alpha Team

A learning-focused Django project built by following the official
[Django tutorial](https://docs.djangoproject.com/en/5.2/intro/tutorial01/).  
It implements a simple polling application where users can browse questions using tiles visuals,
cast votes, and view results rendered as a bar chart using the native HTML
`<progress>` element.



> **Purpose** — This repository is a warm-up educational exercise. The goal is
> to get familiar with Django's core concepts: models, views, templates, URL
> routing, the ORM, static files, and automated testing.

> **Purpose** — This repository is a warm-up educational exercise. The goal is
> to get familiar with Django's core concepts: models, views, templates, URL
> routing, the ORM, static files, and automated testing.
## Table of Contents

1. [Project structure](#1-project-structure)
2. [Environment setup](#2-environment-setup)
3. [Running the development server](#3-running-the-development-server)
4. [Database migrations](#4-database-migrations)
5. [Django Debug Toolbar](#5-django-debug-toolbar)
6. [Running tests](#6-running-tests)
7. [Git workflow & branches](#7-git-workflow--branches)

---

## 1. Project structure

```
polls-alpha/
├── mysite/                  ← Django project root (manage.py lives here)
│   ├── mysite/              ← Project-level settings, URLs, WSGI
│   │   ├── settings.py
│   │   └── urls.py
│   └── polls/               ← The polls Django app
│       ├── migrations/
│       ├── templates/polls/
│       ├── static/polls/
│       ├── models.py        ← Question & Choice models
│       ├── views.py         ← Index, Detail, Results, vote()
│       ├── urls.py
│       └── tests.py
├── venv/                    ← Local virtual environment (not committed)
├── requirements.txt
└── .env.example             ← Template for required environment variables
```

---

## 2. Environment setup

### 2.1 Create and activate the virtual environment

Run these commands once from the `polls-alpha/` directory.

```bash
# Create the virtual environment
python3 -m venv venv

# Activate it (macOS / Linux)
source venv/bin/activate

# Activate it (Windows – PowerShell)
# venv\Scripts\Activate.ps1
```

You should see `(venv)` prepended to your shell prompt when active.

### 2.2 Install dependencies

```bash
pip install -r requirements.txt
```

### 2.3 Set the SECRET_KEY environment variable

Django refuses to start without a `SECRET_KEY`. It is intentionally **not**
hard-coded — never commit a real key to version control.

**Option A — export in the current shell session (quickest for development):**

```bash
# Use double quotes on macOS/zsh to avoid shell interpretation issues
export SECRET_KEY="replace-this-with-a-long-random-string"
```

**Option B — add to your shell profile so it persists across sessions:**

```bash
# Append to ~/.zshrc (or ~/.bashrc)
echo 'export SECRET_KEY="replace-this-with-a-long-random-string"' >> ~/.zshrc
source ~/.zshrc
```

**Option C — generate a fresh key with Django's utility:**

```bash
python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"
```

Copy the output and use it as the value in Option A or B.

> **Tip:** See `.env.example` for the variable name reference.

---

## 3. Running the development server

All `manage.py` commands must be run from the `mysite/` directory (where
`manage.py` lives) with the virtual environment active and `SECRET_KEY`
exported.

```bash
cd mysite
python manage.py runserver
```

Open [http://127.0.0.1:8000/polls/](http://127.0.0.1:8000/polls/) in your browser.

The admin interface is available at
[http://127.0.0.1:8000/admin/](http://127.0.0.1:8000/admin/).

---

## 4. Database migrations

The project uses **SQLite** (file `mysite/db.sqlite3`) in development — no
database server is required.

### Apply all pending migrations (first-time setup or after pulling changes)

```bash
cd mysite
python manage.py migrate
```

### Create new migrations after modifying `models.py`

```bash
python manage.py makemigrations polls
python manage.py migrate
```

### Create a superuser for the admin panel

```bash
python manage.py createsuperuser
```

> `db.sqlite3` is listed in `.gitignore` and is not committed — run
> `migrate` fresh in each new environment.

---

## 5. Django Debug Toolbar

[django-debug-toolbar](https://django-debug-toolbar.readthedocs.io/) is
loaded **only in non-test runs** (`DEBUG=True` and not executing the test
runner). It renders a sidebar with SQL queries, template context, request
headers, and more.

### Install

```bash
pip install django-debug-toolbar
```

After installing, freeze the updated requirements:

```bash
pip freeze > requirements.txt
```

### How it is wired up

`settings.py` adds the app and middleware conditionally:

```python
# settings.py (excerpt)
INTERNAL_IPS = ["127.0.0.1"]

TESTING = "test" in sys.argv or "PYTEST_VERSION" in os.environ

if not TESTING:
    INSTALLED_APPS += ["debug_toolbar"]
    MIDDLEWARE.insert(1, "debug_toolbar.middleware.DebugToolbarMiddleware")
```

`urls.py` mounts the toolbar URLs when `DEBUG` is `True`:

```python
# urls.py (excerpt)
if settings.DEBUG:
    import debug_toolbar
    urlpatterns += [path("__debug__/", include(debug_toolbar.urls))]
```

The toolbar panel appears automatically on every page when you visit the
site in a browser from `127.0.0.1`.

---

## 6. Running tests

All tests live in `polls/tests.py`. Run them from the `mysite/` directory
with the virtual environment active.

### Run the full test suite

```bash
cd mysite
python manage.py test polls
```

### Run a specific test class

```bash
python manage.py test polls.tests.QuestionBarChartViewTests --verbosity=2
```

### Run a single test method

```bash
python manage.py test polls.tests.QuestionBarChartViewTests.test_progress_bar_exist --verbosity=2
```

### Test classes at a glance

| Class | What it covers |
|---|---|
| `QuestionModelTests` | `was_published_recently()` edge cases |
| `QuestionIndexViewTests` | Index page: past/future questions, ordering |
| `QuestionDetailViewTests` | Detail view: 404 on future, 200 on past |
| `QuestionBarChartViewTests` | Results page: `<progress>` tag and `.tile` CSS class |

> **Note:** Because `SECRET_KEY` is read from the environment, the variable
> must be exported before running tests too. Alternatively, prefix the
> command inline:
>
> ```bash
> SECRET_KEY="any-value-works-for-tests" python manage.py test polls
> ```

---

## 7. Git workflow & branches

### Branch naming conventions used in this repo

| Prefix | Purpose |
|---|---|
| `main` | Stable, reviewed code |
| `feature/` | New functionality (e.g. `feature/bar-chart-result`) |
| `fix/` | Bug fixes (e.g. `fix/index-never-cache`) |
| `docs/` | Documentation-only changes |

### Everyday workflow

```bash
# 1. Make sure main is up to date
git checkout main
git pull origin main

# 2. Create a new feature branch
git checkout -b feature/your-feature-name

# 3. Work, commit in small logical steps
git add .
git commit -m "feat: short description of what changed"

# 4. Push the branch and open a Pull Request
git push origin feature/your-feature-name
```

### Useful git commands

```bash
# See all local and remote branches
git branch -a

# Switch to an existing branch
git checkout feature/bar-chart-result

# Pull latest changes from the remote for the current branch
git pull

# View a compact log with branch graph
git log --oneline --all --graph

# Check what has changed before committing
git status
git diff
```

### Commit message style

Follow the [Conventional Commits](https://www.conventionalcommits.org/) convention:

```
<type>: <short summary>

feat:     a new feature
fix:      a bug fix
docs:     documentation only
test:     adding or updating tests
refactor: code change that neither fixes a bug nor adds a feature
style:    formatting, whitespace (no logic change)
chore:    maintenance (deps, config, etc.)
```

Example:

```
feat: add bar chart to results page using <progress> element
```