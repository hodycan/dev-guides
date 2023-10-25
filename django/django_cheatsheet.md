# cheatsheet.md

## server

`$ python manage.py runserver`

## migrations

`$ python manage.py makemigrations [app]`

`$ python manage.py sqlmigrate [app] 0001`

`$ python manage.py migrate`

## validation
`$ python manage.py check`

## testing
server must be running

`$ python manage.py tests [app]`

## debug checklist
1. urls
2. views
3. templates
4. models

## database api

### lookup

`Question.objects.all()`

`Question.objects.filter(id=1)`

`Question.objects.filter(question_text__startswith="What")`

`Question.objects.get(pub_date__year=current_year)`

`Question.objects.get(pk=1)`

### related objects

`q.choice_set.all()`    

`Question.objects.get(pk=1)`

`q.choice_set.create(choice_text="Not much", votes=0)`

`q.choice_set.count()`