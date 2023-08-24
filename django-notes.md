# 1- Setting up a Django project
## 1-1- Creating a Django project
```
django-admin startproject [project-name] .
```

## 1-2- Creating a new app in the current project folder
```
django-admin startup [app-name] 
```

## 1-3- Creating a new app in the current project folder
```
django-admin startup [app-name] 
```
**Note:** After creating the app, we should register it in the settings.py file of the main project folder (inside the INSTALLED_APPS list, just insert an entry of the name of our newly created app.)

## 1-4- Activating a virtual environment
```
. /usr/env/bin/activate
```

## 1-5- Running Django server
```
python manage.py runserver 0.0.0.0:8000 
```

**Note:** This command should be executed in the project's folder.
