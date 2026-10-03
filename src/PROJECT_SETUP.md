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

GitLab is configured to use: src/.gitlab-ci.yml

It will automatically check for any issues.

---
