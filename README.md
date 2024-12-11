# Django User Authentication Application

## Overview
This Django application demonstrates a basic user authentication system, including user signup and a home page accessible only to authenticated users.

## Features
- User signup functionality using Django's `UserCreationForm`.
- Protected home page accessible only to logged-in users.
- Redirect to the login page upon successful signup.

## Requirements
- Python 3.x.
- Django (>=3.x).

## Installation

### 1. Clone the Repository
```bash
git clone <repository_url>
cd <repository_folder>
```

### 2. Install Dependencies
Ensure you have `pip` installed. Install the required Django package:
```bash
pip install django
```

### 3. Set Up the Project
Create a Django project and integrate the app:
```bash
django-admin startproject myproject
cd myproject
python manage.py startapp myapp
```
Replace the `views.py` file in your app directory with the provided code snippet.

### 4. Configure URLs
Update the `urls.py` files as follows:

#### `myproject/urls.py`
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('myapp.urls')),  # Include app-specific URLs
]
```

#### `myapp/urls.py` (create this file if it does not exist)
```python
from django.urls import path
from . import views

app_name = 'base'

urlpatterns = [
    path('', views.home, name='home'),
    path('signup/', views.authView, name='signup'),
]
```

### 5. Set Up Templates
Create the following directory structure in your app:
```plaintext
myapp/
├── templates/
    ├── registration/
        └── signup.html
    └── home.html
```

#### Example `signup.html`
```html
<!DOCTYPE html>
<html>
<head>
    <title>Signup</title>
</head>
<body>
    <h1>Signup</h1>
    <form method="post">
        {% csrf_token %}
        {{ form.as_p }}
        <button type="submit">Sign Up</button>
    </form>
</body>
</html>
```

### 6. Apply Migrations
Run the following commands to set up the database:
```bash
python manage.py makemigrations
python manage.py migrate
```

### 7. Run the Server
Start the development server:
```bash
python manage.py runserver
```
Visit `http://127.0.0.1:8000/signup/` to access the signup page.

## Usage
- Navigate to `/signup/` to register a new user.
- After successful registration, you will be redirected to the login page.
- Log in to access the protected home page at `/`.

## Notes
- Configure `LOGIN_URL` in `settings.py` to point to your login URL:
```python
LOGIN_URL = '/login/'
```
- Add proper styling and error handling as required.
- Extend the `UserCreationForm` if you need to collect additional user information during signup.
