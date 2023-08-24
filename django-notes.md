## Creating a Django project
```
django-admin startproject [project-name] .
```

## Creating a new app in the current project folder
```
django-admin startup [app-name] 
```

## Creating a new app in the current project folder
```
django-admin startup [app-name] 
```
*Note*: After creating the app, we should register it in the settings.py file of the main project folder (inside the INSTALLED_APPS list, just insert an entry of the name of our newly created app.)

## Activating a virtual environment
```
. /usr/env/bin/activate
```

## Running Django server
```
python manage.py runserver 0.0.0.0:8000 
```

*Note:* this command should be executed in the project's folder.
