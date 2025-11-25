---
---

# django reference

https://docs.djangoproject.com/en/4.2/intro/tutorial01/

See also:

- Database
- Fields


setting up new project
----------------------

#### create and activate venv
`python3 -m venv .venv`
`source .venv/bin/activate`

#### pip install django
`pip install django`

#### create project
`$ django-admin startproject PROJECT_NAME`

#### run server
`python manage.py runserver`


#### create app 

inside PROJECT_NAME
`$ python manage.py startapp core`

add app to INSTALLED_APPS in settings.py
`{APP}.apps.{APP}Config`


#### default apps databases

either 

1. migrate with `$ python manage.py migrate`

or 2. comment out the apps in settings.py


#### start server

CLI in site directory  
`$ python manage.py runserver`

server running at `http://127.0.0.1:8000/`  
or `http://localhost:8000/`



handling requests: views and urls
---------------------------------

#### views

- views are defined in `MY_APP.views`.
- django routes requests from a `url` to a corresponding `view` 
- `view` then returns `django.http.HttpResponse`
    - eventually should always use `render` instead though.

- add these imports in new view files
    - `from django.http import HttpResponse`
    - `from django.shortcuts import render`

#### urls

import `from . import views`

create url patterns in `APP_NAME/urls.py`

include patterns in the site's root URLconf `SITE_NAME/urls.py`.
    - e.g. `path("", include("pb_app.urls"))`

#### templates

in views
`return render(request, "APP/TEMPLATE.html", context)`

put templates in 
`APP/templates/APP/`

#### `django.url.path` arguments

route
: url pattern. Patterns don’t search GET and POST parameters

view
: httprequests sent here with the parameters

    