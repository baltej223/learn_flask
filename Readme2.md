This File only focus on **RENDERING TEMPLATES**

# Rendering Templates using Flask: Comprehensive Documentation

## Introduction

Flask is a lightweight and flexible web framework for Python, designed to make web development simple and easy. One of its key features is its robust templating engine, which enables developers to build dynamic and interactive web pages efficiently. In this comprehensive documentation, we will delve into various aspects of rendering templates using Flask, covering not only the basics but also advanced topics such as template inheritance, passing data to templates, using control structures, and more.

## Table of Contents

1. **Setting Up Flask Application**
2. **Creating and Organizing Templates**
3. **Rendering Basic Templates**
4. **Passing Data to Templates**
5. **Template Inheritance**
6. **Using Control Structures in Templates**
7. **Including External CSS and JavaScript**
8. **Handling Forms in Templates**
9. **Template Context Processors**
10. **Best Practices and Tips**

Let's explore each of these topics in detail.

---

## 1. Setting Up Flask Application

Before we dive into rendering templates, let's set up a basic Flask application.

### Prerequisites

Make sure you have Python installed on your system.

Install Flask using pip:

```bash
pip install Flask
```

### Creating a Flask Application

Create a new Python file, let's call it `app.py`, and add the following code:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(debug=True)
```

This code sets up a basic Flask application with a single route (`/`) that returns "Hello, World!".

Run the Flask application:

```bash
python app.py
```

Visit `http://127.0.0.1:5000/` in your web browser to see the application running.

---

## 2. Creating and Organizing Templates

Flask uses the Jinja2 templating engine by default. Templates are HTML files with embedded Jinja2 expressions, which allow for dynamic content generation.

### Setting Up Templates Directory

Create a directory named `templates` in the same directory as your `app.py` file. Flask will automatically look for templates in this directory.

```
project/
│
├── app.py
└── templates/
    └── index.html
```

### Creating a Template

Inside the `templates` directory, create a new HTML file named `index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Flask App</title>
</head>
<body>
    <h1>Hello, {{ name }}!</h1>
</body>
</html>
```

This template contains a placeholder `{{ name }}` which will be replaced with actual data when rendered.

---

## 3. Rendering Basic Templates

Now, let's render the `index.html` template using Flask.

### Rendering Templates

Modify the `index` route in your `app.py` file as follows:

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html', name='User')

if __name__ == '__main__':
    app.run(debug=True)
```

Here, we use the `render_template` function from Flask to render the `index.html` template. We pass the `name` variable as a keyword argument.

Restart the Flask application and visit `http://127.0.0.1:5000/` to see the rendered template.

---

## 4. Passing Data to Templates

You can pass data dynamically to templates by providing additional keyword arguments to the `render_template` function.

### Example: Passing User Data

```python
@app.route('/user/<name>')
def user(name):
    return render_template('user.html', name=name)
```

In this route, the `name` parameter is dynamically passed to the `user.html` template.

---

## 5. Template Inheritance

Template inheritance allows you to create base templates and extend them in other templates, facilitating code reusability and maintainability.

### Example: Base Template

**base.html**:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}{% endblock %}</title>
</head>
<body>
    {% block content %}{% endblock %}
</body>
</html>
```

**child.html**:

```html
{% extends "base.html" %}

{% block title %}
    Welcome
{% endblock %}

{% block content %}
    <h1>Hello, {{ name }}!</h1>
{% endblock %}
```

In this example, `child.html` extends `base.html` and overrides the `title` and `content` blocks.

---

## 6. Using Control Structures in Templates

Jinja2 templates support various control structures such as loops and conditionals, allowing for dynamic content generation based on logic.

### Example: Looping Through Data

```html
<ul>
    {% for item in items %}
        <li>{{ item }}</li>
    {% endfor %}
</ul>
```

In this example, we iterate over a list of `items` and generate list items dynamically.

---

## 7. Including External CSS and JavaScript

You can include external CSS and JavaScript files in your templates to enhance the styling and functionality of your web pages.

### Example: Including CSS

```html
<link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
```

Here, `styles.css` is a CSS file located in the `static` directory of your Flask project.

---

## 8. Handling Forms in Templates

Flask provides built-in support for handling forms in templates using the `Flask-WTF` extension.

### Example: Form Handling

```python
from flask_wtf import FlaskForm
from wtforms import StringField, SubmitField

class MyForm(FlaskForm):
    name = StringField('Name')
    submit = SubmitField('Submit')
```

In the template:

```html
<form method="POST" action="">
    {{ form.csrf_token }}
    {{ form.name.label }}
    {{ form.name() }}
    {{ form.submit() }}
</form>
```

---

## 9. Template Context Processors

Template context processors allow you to inject additional variables into all templates, making them accessible without explicitly passing them in each render call.

### Example: Context Processor

```python
@app.context_processor
def inject_user():
    user = get_current_user()  # Example function to retrieve current user
    return dict(user=user)
```

Now, the `user` variable will be available in all templates without explicitly passing it.

---
