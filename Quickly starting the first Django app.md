# Quickly starting the first Django app
**Creating a project**
From the command file, ``cd`` into a directory where you'd like to store your code, the  run the following command:
```shell
sudo django-admin startproject AIMSF
```
> __Note:__
> This will auto-generate some code that establishes a Django project - a collection of settings for an instance of Django, in the __AIMSF__ directory, including database configuration, Django-specific options and application-specific settings.
> Let's look at what ``startproject`` created:
> ``AIMSF/``
``├── AIMSF``
``│   ├── __init__.py``
``│   ├── settings.py``
``│   ├── urls.py``
``│   └── wsgi.py``
``└── manage.py``
> These files are:
> * The outer __AIMSF/__ root directory is just a container for your project, and you can rename it to anything you like.
> * __manage.py__: A command-line utility that lets you interact with this Django project in various ways, such as operating database.
> * **\_\_init\_\_.py**: An empty file that tells Python that this directory should be considered a Python package.
> * __setting.py__: Setting/configuration for this Django project.
> * __urls.py__: The URL declarations for this Django project; a "table of contents" of your Django-powered site.
> * __wsgi.py__: An entry-point for WSGI(Web Server Gateway Interface)-compatible web servers to serve your project. 

---
__The development server__
 Change into the outer __AIMSF__ directory, if you have not already, and run the following commands:
 ```shell
 sudo python3 manage.py runserver
```
Now that the server's running, visit [_http:127.0.0.1:8080_](http:127.0.0.1:8080) with your Web browser.
> __Note:__
> By default, the ``runserver`` command starts the development server on the internal IP at port 8000.
> You can change the port to 8080 by run the following code:
> ```shell
> sudo python3 manage.py runserver 8080
> ```
> As well as you can change the IP to a available one, use:
> ```shell
> sudo python3 manage.py runserver 192.168.0.100:8080
> ```
