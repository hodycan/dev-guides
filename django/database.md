---
---

# database_reference.md

https://docs.djangoproject.com/en/4.2/intro/tutorial01/

<br>

PostgreSQL Initial Setup
------------------------

#### update settings for postgres
in SITE_NAME/settings.py, DATABASES engine should be updated from SQLite to PostgreSQL and configured to connect to the local postgresql database and server.

```
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": "parkingbuddy",
        "USER": "admin",
        "PASSWORD": "password", # TODO reconsider database credentials?
        "HOST": "localhost",
        "PORT": "5432",
    }
}
```

#### pre-installed apps and databases

Upon initial setup of postgresql, databases included with default pre-installed apps must be migrated, in order to use them, create the tables in the postgresql server with:

`$ python manage.py migrate`

  
<br>

Models and Migration
--------------------

With Model definitions, Django can 
- Create and update database schema
- Create python database-access API for accessing models' objects

Update postgres tables and schema via Django using definitions in APP_NAME.models.

#### Include app in project
Reference app's configuration class in INSTALLED_APPS setting. Only need to do this one.

- Add `{APP_NAME}.app.{APP_NAME}Config` to `{SITE_NAME}.settings.INSTALLED_APPS`

#### Store changes as a migration
Tells django you've made changes to your models (or you've made some new models). 

`$ python manage.py makemigrations [app]`

#### Preview migration SQL commands
`$ python manage.py sqlmigrate [app] 0001`


#### Validate project code
`$ python manage.py check`


#### migrate the changes
`$ python manage.py migrate`

Notes:

- Table names are generated with all-lowercase {app name}_{model name}
_ `_id` appended to end of foreign key field name


<br>


Database API
------------

#### List all objects of a model
`{Model}.objects.all()`

#### Create object
`q = Question(question_text="What's new?", pub_date=timezone.now())`

#### Save model into database
`q.save()`

#### Model ID
`q.id`

#### Access and modify model field values as Python attributes
`q.question_text`

`q.question_text = "What's up?"`

`q.save()`


#### Model.__str__

```
class Question(models.Model):
    # ...
    def __str__(self):
        return self.question_text
```

#### Model custom methods

```
class Question(models.Model):
    # ...
    def was_published_recently(self):
        return self.pub_date >= timezone.now() - datetime.timedelta(days=1)
```

#### Lookup objects
`Question.objects.filter(id=1)`

`Question.objects.filter(question_text__startswith="What")`

`Question.objects.get(pub_date__year=current_year)`

`Question.objects.get(pk=1)`


#### Related objects
Django creates a set to hold the "other side" of a ForeignKey relation

`q.choice_set.all()`    

`Question.objects.get(pk=1)`

`q.choice_set.create(choice_text="Not much", votes=0)`

`q.choice_set.count()`


#### Lookup follows relationships as far as needed
`Choice.objects.filter(question__pub_date__year=current_year)`



