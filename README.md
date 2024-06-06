# Learn Flask

Flask from scratch is quite a journey! Let's break it down step by step. We'll start with the basics and gradually move to more advanced topics. Here's a rough outline of what we'll cover:

1. Introduction to Flask
2. Setting up Flask
3. Flask Basics:
   - Creating a Basic Flask App
   - Routes and Views
   - Templates and Jinja2
   - Request and Response Handling
   - Static Files
   - Using Forms
4. Example Projects

Let's dive in!

### 1. Introduction to Flask

Flask is a lightweight WSGI web application framework written in Python. It's designed to make getting started quick and easy, with the ability to scale up to complex applications. Flask provides the tools needed to build a web application, but it doesn't enforce any dependencies or project structure.

### 2. Setting up Flask

To get started with Flask, you'll need to install it. You can use pip, Python's package manager, to install Flask:

```bash
pip install Flask
```

Once Flask is installed, you can start building your first Flask application.

### 3. Flask Basics

#### Creating a Basic Flask App

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(debug=True)
```

#### Routes and Views

Routes define the URLs of your application and the functions that handle them.

```python
@app.route('/')
def index():
    return 'Index Page'

@app.route('/hello')
def hello():
    return 'Hello, World!'
```

#### Templates and Jinja2

Templates allow you to separate the presentation layer from your Python code.

```python
from flask import render_template

@app.route('/user/<username>')
def show_user_profile(username):
    return render_template('user.html', username=username)
```

#### Request and Response Handling

Flask provides request and response objects to handle HTTP requests and responses.

```python
from flask import request, jsonify

@app.route('/api', methods=['POST'])
def api():
    data = request.get_json()
    # Process the data
    return jsonify({'result': 'success'})
```

#### Static Files

Static files like CSS, JavaScript, and images can be served using Flask.

```python
@app.route('/static/<path:path>')
def static_file(path):
    return app.send_static_file(path)
```

#### Using Forms

Flask-WTF extension is commonly used for handling forms in Flask applications.

```python
from flask_wtf import FlaskForm
from wtforms import StringField, SubmitField
from wtforms.validators import DataRequired

class MyForm(FlaskForm):
    name = StringField('Name', validators=[DataRequired()])
    submit = SubmitField('Submit')
```


SW4gYXJvdW5kIDUwMDAwIHdvcmRzLCBUZWFjaCBtZSBmbGFzayBmcm9tIHNjcmF0Y2guIFlvdXIgdGVhY2hpbmcgc2hvdWxkIGluY2x1ZGUgYmFzaWNzIG9mIGZsYXNrLCB3b3JraW5nIG9mIGZsYXNrLCBkZWZpbmUgYmFzaWMgZnVuY3Rpb24gb2YgZmxhc2ssIGFuZCBhbHNvIGluY2x1ZGUgYWR2YW5jZSB0b3BpY3Mgb2YgZmxhc2sgd2l0aCBleGFtcGxlcw==

```Made by Baltej Singh```
