
## template boiler plate

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Page Title</title>
  </head>


  <body>
    <div class="navbar">
      {% block navbar %}{% endblock %}
    </div>

    <div class="content">
      {% block content %}{% endblock %}
    </div>


  </body>
</html>
```