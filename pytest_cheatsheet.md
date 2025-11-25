
## install packages

`pip install pytest pytest-django`

## add to requirements

```
pytest
pytest-django
```

## create pytest.init at project root

```
[pytest]
DJANGO_SETTINGS_MODULE = config.settings
pythonpath = .
```

## create tests/ dir

```
project/
  app/
  config/
  tests/
    test_models.py
  manage.py
  pytest.init
```

## run tests

`pytest`

verbose, stop with first fail, summary at bottom:

`pytest -vv --maxfail=1 -ra`

for full and exact stack trace:

`pytest -vv --full-trace -ra`

## reminders

Mark tests that hit the database with `@pytest.mark.django_db`
