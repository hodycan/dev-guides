# django deployment checklist

overview:

1. gunicorn
2. environment variables
3. static files + whitenoise
4. database set up (if applicable
5. requirements.txt

## 1. prep

in django project root (not git repo root):

- activate virtual environment: `source .venv/bin/activate`
- gunicorn server: `pip install gunicorn`
- environment variables: `pip install python-dotenv`
- static files: `pip install whitenoise`

if using postgres on render:

- `pip install psycopg2-binary`
- `pip install dj-database-url`

**create Procfile**

create `Procfile` in project root, same folder as `manage.py`

contents: `web: gunicorn [PROJECT_NAME].wsgi`

## 2. create .env 

add for each environment variable:

`VARIABLE=VALUE`

e.g. `DEBUG=True`

import to render

## 2. update settings.py


**set up python-dotenv**

- `from pathlib import Path`
- `from dotenv import load_dotenv`

update environment variables to .env definitions:

`DEBUG = os.getenv("DEBUG", "False") == "True"`

**allowed hosts**

`ALLOWED_HOSTS = ["app-name.onrender.com", "localhost", "127.0.0.1"]`

**for static files**


```
MIDDLEWARE = [
    "whitenoise.middleware.WhiteNoiseMiddleware",
    ...
]
```

> add after `django.middleware.security.SecurityMiddleware`

set up static file directories:

- `STATIC_URL = "/static/"`
- `STATIC_ROOT = BASE_DIR / "staticfiles"`

```
STATICFILES_DIRS = [
    BASE_DIR / "static",  # create this if you keep assets here
]
```

```
STORAGES = {
    "staticfiles": {
        "BACKEND": "whitenoise.storage.CompressedManifestStaticFilesStorage"
    }
}
```

### for databases

```
import dj_database_url

DATABASES = {
    "default": dj_database_url.config(
        default=os.getenv("DATABASE_URL"),
        conn_max_age=600,
        ssl_require=True
    )
}
```

## 3. freeze requirements

- `pip freeze > requirements.txt`

## 4. deployment

in render settings:

- set root directory to django root
- build command: `pip install -r requirements.txt && python manage.py collectstatic --noinput`
- start command: `gunicorn DJANGO_PROJECT_NAME.wsgi:application --bind 0.0.0.0:$PORT`






