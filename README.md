# Py App

Welcome to a sample Django Project

# Branch Concepts

### CREATE a new branch for example called fixs/doc

git checkout -b fixes/main-pages

Switched to a new branch 'fixes/main-pages'

This readMe file has some tips for you :)

update: 753

git fetch origin
git checkout main
git pull origin main
git merge origin/fixes/main-pages

# Resolve any merge conflicts if prompted

git add .
git commit

# PUSH branch into MAIN

git push origin main

## Options based on your future plans for the branch:

1. **Keep the Branch**:

   - If you anticipate making more changes or updates related to the `fixs/doc` branch, it's a good idea to keep it. This way, you can continue working on it without creating a new branch each time.

2. **Delete the Branch**:
   - If you believe the work on this branch is complete and you don't need it anymore, you can delete it to keep your repository clean and organized.

Here are the commands to delete the branch both locally and remotely if you decide to remove it:

### Delete the Local Branch

```sh
git branch -d fixs/doc
```

- If the branch hasn't been fully merged, use `-D` to force delete:

```sh
git branch -D fixs/doc
```

### Delete the Remote Branch

```sh
git push origin --delete fixs/doc
```

## Package Management

https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry

# Removing a Branch

⚡angel ❯❯ git checkout main

Already on 'main'
Your branch is up to date with 'origin/main'.

⚡angel ❯❯ git branch -d branch_name

error: branch 'branch_name' not found

⚡angel ❯❯ git branch -d feature-update-home-about

error: the branch 'feature-update-home-about' is not fully merged
hint: If you are sure you want to delete it, run 'git branch -D feature-update-home-about'
hint: Disable this message with "git config advice.forceDeleteBranch false"

⚡angel ❯❯ git branch -D feature-update-home-about

Deleted branch feature-update-home-about (was a3b9051).

⚡angel ❯❯ git push origin --delete feature-update-home-about

To https://github.com/akenel/akd-django-web-app.git

- [deleted] feature-update-home-about

#### Branch successfully removed

## Initial Setup

### Example: akd-django-web-app

- **Image**: `py_app_local_django:latest`

1. **Create Virtual Environment**:

   ```sh
   python -m venv venv
   venv/scripts/activate
   ```

2. **Run Cookiecutter**:

   ```sh
   pipx run cookiecutter https://github.com/cookiecutter/cookiecutter-django.git
   cd <project_slug>  # For example, cd py_app
   ```

3. **Initialize Git Repository**:
   ```sh
   git init
   pip install -r requirements/local.txt
   pip install pre-commit
   pre-commit install
   ```

## Running Tests

### MyPy Sanity Check

- **Command**:
  ```sh
  docker compose -f docker-compose.local.yml run --rm django mypy py_app
  ```
- **Expected Result**: Success: no issues found in 36 source files

### Test Coverage

1. **Run Tests**:

   ```sh
   docker compose -f docker-compose.local.yml run --rm django coverage run -m pytest
   ```

2. **Generate Coverage Report**:

   ```sh
   docker compose -f docker-compose.local.yml run --rm django coverage html
   ```

3. **Review Coverage Report**:
   ```sh
   cd htmlcov
   Invoke-Item "index.html"
   ```

- **Expected Coverage**: 80%+ OK

## Pre-Commit Hooks

1. **Set Up Pre-Commit**:
   ```sh
   git init
   git add --all
   pre-commit install
   pre-commit --version
   pre-commit run --all-files
   ```

## Git Workflow

### Initial Commit

1. **Set Up Repository**:
   ```sh
   git remote add origin https://github.com/akenel/pyWeb-app.git
   git branch -M main
   git push -u origin main
   ```

### Creating and Pushing Changes

1. **Create a New Branch**:

   ```sh
   git checkout -b feature-update-home-about
   ```

2. **Make and Commit Changes**:

   ```sh
   git add .
   pre-commit run --all-files
   git commit -m "Update home and about pages with new API call"
   ```

3. **Push Changes**:
   ```sh
   git push -u origin feature-update-home-about
   ```

## Additional Information

### Execute Management Commands

- **Commands**:
  ```sh
  docker compose -f docker-compose.local.yml run --rm django python manage.py migrate
  docker compose -f docker-compose.local.yml run --rm django python manage.py createsuperuser
  ```

### Basic Commands

- **Install Development Requirements**:

  ```sh
  cd <project_slug>
  python.exe -m pip install --upgrade pip
  pip install -r requirements/local.txt
  git init
  pip install pre-commit
  pre-commit install
  ```

- **Set Environment Variables**:

  ```sh
  $env:COMPOSE_FILE="docker-compose.local.yml"
  $env:DATABASE_URL="postgresql://debug:debug@postgres:5432/py_app"
  ```

- **Start Docker Containers**:
  ```sh
  docker compose up -d
  ```

### Type Checks

- **Run MyPy**:
  ```sh
  docker compose -f docker-compose.local.yml run --rm django mypy py_app
  ```

### Running Tests with Pytest

- **Commands**:
  ```sh
  docker compose -f docker-compose.local.yml run --rm django coverage run -m pytest
  docker compose -f docker-compose.local.yml run --rm django coverage html
  cd htmlcov
  Invoke-Item "index.html"
  ```

### Celery

- **Run Celery Worker**:

  ```sh
  cd py_app
  celery -A config.celery_app worker -l info
  ```

- **Run Celery Beat**:
  ```sh
  cd py_app
  celery -A config.celery_app beat
  ```

### Email Server

- **Access Mailpit**:
  - Open `http://127.0.0.1:8025`

### Deployment with Docker

- See [cookiecutter-django Docker documentation](https://cookiecutter-django.readthedocs.io/en/latest/3-deployment/deployment-with-docker.html).

### Custom Bootstrap Compilation

- **Customize Bootstrap**: Tweak variables in `static/sass/custom_bootstrap_vars`.

[![Built with Cookiecutter Django](https://img.shields.io/badge/built%20with-Cookiecutter%20Django-ff69b4.svg?logo=cookiecutter)](https://github.com/cookiecutter/cookiecutter-django/)
[![Ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff)

License: MIT
