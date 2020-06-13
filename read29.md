[ HOME ](README.md)
# Read 29 - Django Custom User

>  Always use a custom user model for all new Django projects

- The official Django documentation highly recommends using a custom user model for new projects, The reason is if you want to make any changes to the User model down the road, using a custom user model from the beginning makes this quite easy. 

### Setup
```
$ cd ~/Desktop
$ mkdir users && cd users
$ pipenv install django==3.0.3
$ pipenv shell
(users) $ django-admin.py startproject config .
(users) $ python manage.py startapp users
(users) $ python manage.py runserver
```

### AbstractUser vs AbstractBaseUser
There are two modern ways to create a custom user model in Django: AbstractUser and AbstractBaseUser. In both cases we can subclass them to extend existing functionality **however AbstractBaseUser requires much, much more work**.

### Superuser
It's helpful to create a superuser that we can use to login to the admin and test out login/logout. 
```
(users) $ python manage.py createsuperuser
```