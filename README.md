<p align="center">

  <p align="center">
    Full Stack ChatApp Using Django and Django Channels with React.js for frontend
  </p>
</p>

# Full stack django and react.js app for my interview as a programming instructor.



This app implements chat app using django and django channels which enables django through asgi (web server gateway interface) to use web socket for real-time processes. In other words, with the implementation of django channels, I am able to build a django application that does not load the server side with request by the client app, I also extended the functionality of the app by implementing the client side using react.js. A client side javascript framework that is based on a single page application implimentation, does't load the broswer on page change or routing into another page. It's a wonderful framework I've used for many projects.

To run the backend, run:

```json
virtualenv env
source env/bin/activate
pip install -r requirements.txt
python manage.py runserver
```

To run the frontend:

```json
npm i
npm start
```

To develop locally:

```
1. Change the `DEBUG` flag in `src/settings.js`
2. Create two users (easiest way might be to run `python manage.py createsuperuser` twice)
3. Using django admin, create a `Contact` object for each user.
4. Make sure you have an instance of redis running. 
```

To build for deployment:

```json
npm run build
```

```
Django project setup and django channels inclusion in the project!
```

```
In my terminal or command prompt I create a new folder for my project by running the following command:

mkdir justchat
Navigate to the project folder by running the following command:


cd justchat
Create a new virtual environment for your project by running the following command:


python -m venv venv
Activate the virtual environment by running the following command:

source venv/bin/activate
Install Django by running the following command:


pip install django
Install PostgreSQL by running the following command:

sudo apt-get install postgresql
Create a new PostgreSQL database by running the following command:

sudo -u postgres createdb NEWCHATAPP
Install the PostgreSQL adapter for Python by running the following command:

pip install psycopg2-binary
In the justchat folder, create a new file called .env and add the following code, replacing the values with your own:

DB_NAME=NEWCHATAPP
DB_USER=username
DB_PASSWORD=password
DB_HOST=127.0.0.1
DB_PORT=5432
SECRET_KEY=your_secret_key
In the justchat folder, I created a new file called .gitignore and added the following code:


venv/
__pycache__/
*.pyc
*.pyo
*.env
*.log
This will prevent the .env file from being pushed to my version control system.

Create a new Django project by running the following command

django-admin startproject justchat
Navigate to the project folder by running the following command:

cd justchat
Create a new Django app by running the following command:

python manage.py startapp chat
Install Django Channels by running the following command:

pip install channels
In the justchat folder, open the settings.py file and add the following code to the INSTALLED_APPS list:
python

'channels',
'chat',

Install Redis by downloading and installing the appropriate version for my system from the following link: https://redis.io/download

Start Redis by running the redis-server.exe file located in the Redis installation directory.
Still in settings.py, update the DATABASES dictionary to use the PostgreSQL database, by adding the following code:

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.environ.get('DB_NAME'),
        'USER': os.environ.get('DB_USER'),
        'PASSWORD': os.environ.get('DB_PASSWORD'),
        'HOST': os.environ.get('DB_HOST'),
        'PORT': os.environ.get('DB_PORT'),
    }
}
This code uses the environment variables from the .env file to connect to the PostgreSQL database.

Also in settings.py, update the SECRET_KEY variable to use the value from the .env file, by adding the following code:
csharp

SECRET_KEY = os.environ.get('SECRET_KEY')
In the justchat folder, create a new file called routing.py and add the following code:


from channels.routing import ProtocolTypeRouter, URLRouter
```

```
  Working with the ui and also including PARCEL as the application bundler instead of webpack
```

```
I downloaded a chatapp template to speed up development process and configured it into the template located in justchat/static/chatapp.

In the justchat folder, create a new folder called templates and create a new file called base.html inside it. Add the following code to the file:


<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{% block title %}{% endblock %}</title>
    <link rel="stylesheet" href="{% static 'chatapp/css/style.css' %}">
  </head>
  <body>
    {% block content %}{% endblock %}
  </body>
</html>
This code defines a base HTML template that includes the chatapp CSS file.

In the justchat/chat/views.py file, add the following code to the index function:

from django.shortcuts import render

def index(request):
    return render(request, 'chatapp/index.html')
This code renders the chatapp/index.html template.

In the justchat/chatapp folder, create a new file called index.html and add the following code:


{% extends 'base.html' %}

{% block title %}Chat App{% endblock %}

{% block content %}
  <div id="root"></div>
  <script src="{% static 'chatapp/js/app.js' %}"></script>
{% endblock %}
This code extends the base template and includes the React app's root element and JavaScript file.

Install Node.js and npm by downloading and installing the appropriate version for your system from the following link: https://nodejs.org/en/download/

In the justchat folder, initialize a new Node.js project by running the following command:


npm init -y
Install the required npm packages for React by running the following command:


npm install react react-dom
Install Parcel bundler by running the following command:


npm install -g parcel-bundler
In the justchat folder, create a new folder called static_src and a new file called app.js inside it. Add the following code to the file:


import React from 'react';
import ReactDOM from 'react-dom';

const App = () => {
    return (
        <h1>Hello, world!</h1>
    );
};

ReactDOM.render(<App />, document.getElementById('root'));
This code defines a simple React app that displays a "Hello, world!" message.

In the justchat folder, create a new file called .babelrc and add the following code:

{
    "presets": ["@babel/preset-react"]
}
In the justchat folder, compile the React app by running the following command:


parcel build static_src/app.js --out-dir static/chatapp/js/
In the justchat/templates/base.html file, replace the <link> and <script> tags with the following code:


{% load static %}

<link rel="stylesheet" href="{% static 'chatapp/css/style.css' %}">
<script src="{% static 'chatapp/js/app.js' %}"></script>


In the justchat folder, install the django-webpack-loader package by running the following command:

pip install django-webpack-loader
In the justchat/settings.py file, add the following to the INSTALLED_APPS list:


'webpack_loader',
Add the following to the bottom of the settings.py file:


# Webpack loader configuration
WEBPACK_LOADER = {
    'DEFAULT': {
        'BUNDLE_DIR_NAME': 'chatapp/js/',
        'STATS_FILE': os.path.join(BASE_DIR, 'static', 'chatapp', 'webpack-stats.json'),
    }
}
In the justchat/chat/views.py file, change the index function to the following:


from django.shortcuts import render

def index(request):
    return render(request, 'chatapp/index.html', {})
This code passes an empty context dictionary to the template.

In the justchat/chatapp/index.html file, replace the <script> tag with the following code:

{% load render_bundle from webpack_loader %}

<div id="root"></div>
{% render_bundle 'main' %}
This code uses the render_bundle template tag from django-webpack-loader to include the Webpack bundle in the template.

Create a new Django app called accounts by running the following command:


python manage.py startapp accounts
In the justchat/accounts folder, create a new file called forms.py and add the following code:


from django import forms
from django.contrib.auth.forms import UserCreationForm
from django.contrib.auth.models import User

class SignUpForm(UserCreationForm):
    email = forms.EmailField(max_length=254, help_text='Required. Enter a valid email address.')

    class Meta:
        model = User
        fields = ('username', 'email', 'password1', 'password2')
This code defines a SignUpForm form that inherits from UserCreationForm and adds an email field.

In the justchat/accounts/views.py file, add the following code:


from django.contrib.auth import login, authenticate
from django.shortcuts import render, redirect
from .forms import SignUpForm

def signup(request):
    if request.method == 'POST':
        form = SignUpForm(request.POST)
        if form.is_valid():
            user = form.save()
            user.refresh_from_db()
            user.email = form.cleaned_data.get('email')
            user.save()
            raw_password = form.cleaned_data.get('password1')
            user = authenticate(username=user.username, password=raw_password)
            login(request, user)
            return redirect('index')
    else:
        form = SignUpForm()
    return render(request, 'accounts/signup.html', {'form': form})
This code defines a signup view that uses the SignUpForm form to create a new user account.

In the justchat/urls.py file, add the following to the top:

from django.urls import include
Add the following to the urlpatterns list:


path('accounts/', include('django.contrib.auth.urls')),
path('accounts/signup/', views.signup, name='signup'),


In the justchat/templates/base.html file, add the following code to the navigation bar:


<ul class="navbar-nav mr-auto">
    <li class="nav-item">
        <a class="nav-link" href="{% url 'index' %}">Home</a>
    </li>
    {% if user.is_authenticated %}
    <li class="nav-item">
        <a class="nav-link" href="{% url 'logout' %}">Logout</a>
    </li>
    {% else %}
    <li class="nav-item">
        <a class="nav-link" href="{% url 'login' %}">Login</a>
    </li>
    <li class="nav-item">
        <a class="nav-link" href="{% url 'signup' %}">Sign Up</a>
    </li>
    {% endif %}
</ul>
This code adds links to the navigation bar for the login and sign up views.

In the justchat/templates/accounts/signup.html file, add the following code:

{% extends 'base.html' %}

{% block content %}
<h2>Sign up</h2>
<form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Sign up</button>
</form>
{% endblock %}
This code extends the base template and displays the SignUpForm form.

Run the following commands to create the necessary database tables:

python manage.py makemigrations
python manage.py migrate
Start the development server by running the following command:

python manage.py runserver
Open a web browser and navigate to http://localhost:8000/. You should see the chat app with the login and sign up links in the navigation bar.

Sign up for a new account and log in. You should be redirected to the chat app.

```
