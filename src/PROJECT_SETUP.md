# Project Setup & Essential Commands

This project uses:

- **Django** for the web application
- **uv** for Python dependency and virtual environment management
- **Docker** for containerisation
- **GitLab** for version control and CI
- **WSL 2** as the recommended development environment on Windows

---

## 1. Recommended Development Environment

- Run the project from **WSL** rather than PowerShell.
- Docker Desktop should be running on Windows with **WSL integration enabled**.
- Run Git, uv, Django and Docker commands consistently from WSL.

---

## 2. Environment Setup

After cloning the repository, move into the `src` directory:

```bash
cd src
uv sync
docker build -t my-django-app . # or replace my-django-app with whatever you like
docker compose up # Runs container and Django server
```

## 3. Using uv

Install uv in WSL:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh

uv sync
uv add <package-name>
uv remove <package-name>
```

## 4. Using Django

```bash
uv run python manage.py runserver
uv run python manage.py makemigrations
uv run python manage.py migrate
uv run python manage.py check
uv run python manage.py test
```

## 5. Docker

Docker Desktop must be running before using Docker from WSL.

### Build the image

From the `src` directory:

```bash
docker build -t my-django-app .
docker run -p 8000:8000 my-django-app # Run the container
# Useful checks
docker ps # List running containers
docker images # List local images
docker run my-django-app python manage.py check # Run a Django check inside the container:
```

---

## 6. GitLab CI

The root `.gitlab-ci.yml` includes `src/.gitlab-ci.yml`. The existing custom
GitLab CI configuration path `src/.gitlab-ci.yml` also remains supported.

The pipeline runs when a merge request targets `main`, including when new
commits are pushed to that merge request. It installs locked dependencies with
Python 3.12 (matching Docker), runs Django system checks, checks for missing
migrations, applies migrations to SQLite, and runs the Django test suite.
Ordinary branch pushes and merge requests targeting other branches do not run it.

In GitLab, enable **Settings > Merge requests > Merge checks > Pipelines must
succeed** to block merging when the pipeline fails. A runner supporting Docker
images must be available. Protect `main` against direct pushes if all changes
must pass through merge requests.

The current `leap/tests.py` is a placeholder; the pipeline will run application
tests as they are added. Standard merge request pipelines check the source
branch, rather than a simulated merge with `main`.

---
