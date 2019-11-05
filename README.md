*all information in this README.md is courtesy of General Assembly/SEIR*

# DjangoChecklist

## Setup 

- [ ] Start by creating a directory for our project: i.e. ```my_project```
- [ ] Make sure pipenv is installed:

```brew install pipenv```
- [ ] ```cd``` into the ```my_project``` file you created, then run: 

```pipenv install django```
- [ ] Install the library for connecting Django to PostgreSQL:

```pipenv install psycopg2-binary```
- [ ] Open up the project in your favorite text editor
- [ ] Start our Django project (creates a project in the current directory)!

```pipenv run django-admin startproject my_project .```
- [ ] Activate our virtual environment by running ```pipenv shell```

- [ ] Create our app by running ```django-admin startapp myapp``` 

NOTE: You can make myapp whatever you'd like!
NOTE: If django-admin doesn't work, you can replace it with ```python3 manage.py```
- [ ] ```my_project``` is our django project.  ```myapp``` is an "app" inside of this project.

```my_project``` is the base django project where we will handle our routes.  ```myapp``` is where we write our models, controllers, and templates.

## Database Setup

- [ ] Login to psql: 

```$ psql -d postgres```
- [ ] Create a database:
```
> CREATE DATABASE myapp;
> CREATE USER myUser WITH PASSWORD 'user';
> GRANT ALL PRIVILEGES ON DATABASE somedb TO myUser;
> \q
```
OR Create via settings.sql
``` CREATE DATABASE myapp;
CREATE USER myUser WITH PASSWORD 'user';
GRANT ALL PRIVILEGES ON DATABASE somedb TO myUser;
```
Then, in your terminal, run the below command. If you created the database in psql, don't do this step.

``` $ psql -U postgres -f settings.sql ```

- [ ] Navigate to ```my_project/settings.py``` and find the ```DATABASE``` dictionary.  Add the following:

```
DATABASES = {
  'default': {
    'ENGINE': 'django.db.backends.postgresql',
    'NAME': 'myapp',
    'USER': 'myUser',
    'PASSWORD': 'user',
    'HOST': 'localhost'
   }
}
```
To include the app we generated, add the following to the last line of ```INSTALLED_APPS```:

```myapp```

- [ ] In your terminal, run ```python3 manage.py runserver``` and navigate to ```localhost:8000```. You should see a page welcoming you to Django!

- [ ] To see a list of commands that ```manage.py``` offers, type ```python3 manage.py``` in your terminal.

## Models

To create an example python class that inherits from the Django built in ```models.Model``` class, add the following to myapp/models.py:

```
class Example(models.Model):
  name = models.CharField(max_length=100)
  bio = models.CharField(max_length=100)
  photo_url = models.TextField()
  
  def __str__(self):
    return self.name
```

```name```, ```bio```, ```photo_url``` will be represented as columns in our database

## Migrations

- [ ] To migrate this model to the database, first run: 

```$ python3 manage.py makemigrations```
NOTE: Every time you make changes to your models, run ```makemigrations``` again.

- [ ] Once you've made your changes, run: 

```$ python3 manage.py migrate```

- [ ] Open up ```psql```, connect to the ```myapp``` database, and you will see the tables you have created. 


## Django Admin Console
- [ ] In your terminal, run:

```$ python3 manage.py createsuperuser```
- [ ] Fill in the info in the boxes that pop up. 
- [ ] Then, in myapp/admin.py, add the following:

```
from django.contrib import admin
from .models import Example

admin.site.register(Example)
```

- [ ] Then, navigate to localhost:8000/admin and login using the credentials you added in step 2.




