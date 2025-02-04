# Py App

Behold My Awesome Project!

[![Built with Cookiecutter Django](https://img.shields.io/badge/built%20with-Cookiecutter%20Django-ff69b4.svg?logo=cookiecutter)](https://github.com/cookiecutter/cookiecutter-django/)
[![Ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff)

License: MIT

## Execute Management Commands

As with any shell command that we wish to run in our container, this is done using the docker compose -f docker-compose.local.yml run --rm command:
´´´
docker compose -f docker-compose.local.yml run --rm django python manage.py migrate
docker compose -f docker-compose.local.yml run --rm django python manage.py createsuperuser
´´´

## Settings

Moved to [settings](https://cookiecutter-django.readthedocs.io/en/latest/1-getting-started/settings.html).

## Basic Commands

Install development requirements:

$ cd <what you have entered as the project_slug at setup stage>

python.exe -m pip install --upgrade pip
pip install -r requirements/local.txt

git init # A git repo is required for pre-commit to install
pip install pre-commit
pre-commit install

$env:COMPOSE_FILE="docker-compose.local.yml"

docker compose up -d

pre-commit installed at .git\hooks\pre-commit

docker compose -f docker-compose.local.yml up
docker compose -f docker-compose.docs.yml up

Set the DATABASE_URL environment variable
DATABASE_URL environment variable as follows:

env
DATABASE_URL=postgresql://debug:debug@postgres:5432/py_app

Set with PowerShell
$env:DATABASE_URL="postgresql://debug:debug@postgres:5432/py_app"

Here's a breakdown of how this URL is constructed:
Scheme: postgresql://
User: debug
Password: debug
Host: postgres
Port: 5432
Database Name: py_app

Make sure to update your .env file with the new DATABASE_URL before running

# Only if USE_DOCKER environment variable Set to NO

This command should be run via Docker id DOCKER was selected as Yes
$env:DATABASE_URL="postgresql://debug:debug@postgres:5432/py_app"
python manage.py createsuperuser

Execute Management Commands
As with any shell command that we wish to run in our container, this is done using the docker compose -f docker-compose.local.yml run --rm command:

$ docker compose -f docker-compose.local.yml run --rm django python manage.py migrate
$ docker compose -f docker-compose.local.yml run --rm django python manage.py createsuperuser

To run the docs :
docker compose -f docker-compose.docs.yml up

### Setting Up Your Users

- To create a **normal user account**, just go to Sign Up and fill out the form. Once you submit it, you'll see a "Verify Your E-mail Address" page. Go to your console to see a simulated email verification message. Copy the link into your browser. Now the user's email should be verified and ready to go.

- To create a **superuser account**, use this command:

      $ python manage.py createsuperuser

For convenience, you can keep your normal user logged in on Chrome and your superuser logged in on Firefox (or similar), so that you can see how the site behaves for both kinds of users.

### Type checks

Running type checks with mypy:

    $ mypy py_app

# Docker myPy

⚡angel ❯❯ docker compose -f docker-compose.local.yml run --rm django mypy py_app

eg:
docker compose -f docker-compose.local.yml run --rm django mypy py_app
[+] Creating 3/0
✔ Container py_app_local_postgres Running 0.0s
✔ Container py_app_local_mailpit Running 0.0s
✔ Container py_app_local_redis Running 0.0s
wait-for-it: waiting 30 seconds for postgres:5432
wait-for-it: postgres:5432 is available after 0 seconds
PostgreSQL is available
Success: no issues found in 36 source files

### Test coverage

To run the tests, check your test coverage, and generate an HTML coverage report:

    $ coverage run -m pytest
    $ coverage html
    $ open htmlcov/index.html

#### Running tests with pytest

    $ pytest

### Live reloading and Sass CSS compilation

Moved to [Live reloading and SASS compilation](https://cookiecutter-django.readthedocs.io/en/latest/2-local-development/developing-locally.html#using-webpack-or-gulp).

### Celery

This app comes with Celery.

To run a celery worker:

```bash
cd py_app
celery -A config.celery_app worker -l info
```

Please note: For Celery's import magic to work, it is important _where_ the celery commands are run. If you are in the same folder with _manage.py_, you should be right.

To run [periodic tasks](https://docs.celeryq.dev/en/stable/userguide/periodic-tasks.html), you'll need to start the celery beat scheduler service. You can start it as a standalone process:

```bash
cd py_app
celery -A config.celery_app beat
```

or you can embed the beat service inside a worker with the `-B` option (not recommended for production use):

```bash
cd py_app
celery -A config.celery_app worker -B -l info
```

### Email Server

In development, it is often nice to be able to see emails that are being sent from your application. For that reason local SMTP server [Mailpit](https://github.com/axllent/mailpit) with a web interface is available as docker container.

Container mailpit will start automatically when you will run all docker containers.
Please check [cookiecutter-django Docker documentation](https://cookiecutter-django.readthedocs.io/en/latest/2-local-development/developing-locally-docker.html) for more details how to start all containers.

With Mailpit running, to view messages that are sent by your application, open your browser and go to `http://127.0.0.1:8025`

## Deployment

The following details how to deploy this application.

### Docker

See detailed [cookiecutter-django Docker documentation](https://cookiecutter-django.readthedocs.io/en/latest/3-deployment/deployment-with-docker.html).

### Custom Bootstrap Compilation

The generated CSS is set up with automatic Bootstrap recompilation with variables of your choice.
Bootstrap v5 is installed using npm and customised by tweaking your variables in `static/sass/custom_bootstrap_vars`.

You can find a list of available variables [in the bootstrap source](https://github.com/twbs/bootstrap/blob/v5.1.3/scss/_variables.scss), or get explanations on them in the [Bootstrap docs](https://getbootstrap.com/docs/5.1/customize/sass/).

Bootstrap's javascript as well as its dependencies are concatenated into a single file: `static/js/vendors.js`.
