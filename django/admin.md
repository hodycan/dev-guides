# django_admin

$ python manage.py createsuperuser


# polls/admin.py

```
from django.contrib import admin

from .models import Question

admin.site.register(Question)
```