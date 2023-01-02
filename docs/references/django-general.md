# Razzi's Class

Django is used in industry! Pinterest, NASA, Venmo, Sighten, Instagram, etc.

## Overview

- Django is designed to make development fast...
- Razzi: "Django is the present, not the future."
- If you choose an unsupported database, you will be fighting the framework.
- BUT - Django keeps up with internet trends! So it could end up being the future.
- If you are not using a relational database, you may not need Django. It's for working with RDBMS.
- Django can serve REST or GraphQL APIs as well, great backend for modern frontend.
    - For example, Razzi's company switched to Single Page Apps (SPAs) on the frontend with their same django app on the backend (kept old django templates at the time probably)


### Django Benefits

- Out-of-the-box functionality: don't reinvent security, authentication sessions, database access, email...
- Ease of prototyping: easier to start and deploy your project using a well-supported framework
- Scales well to large teams, large projects
    - Django apps make it easy to split up and reuse functionality


### django is the present, not the future

- Designed around rendering html pages
- If you chose an unsupported database, you'll be fighting the framework
- The django framework keeps up with internet trends, though, and now supports asynchronous programming
- Django can serve REST and GraphQL APIs as well, making it a great backend for a modern frontend 


### Django has some premade social networks, we will roll our own
- Vataxia https://github.com/buckyroberts/Vataxia
- Bootcamp https://github.com/vitorfs/bootcamp


#### Our Class Schedule

1. Signup / login / logout (today)
1. Posting (March 5, next Monday)
1. Messaging (March 12)
1. API, static frontend (March 19)


#### First Time Setup

The `manage.py` is executable by default in Python 3.  Simply `./manage.py runserver` or any other argument.

You can `python manage.py runserver 80` for example, to run on any port.

1. Python 3 in a virtualenv
1. pip install django
1. django-admin startproject
1. python manage.py migrate
1. python manage.py createsuperuser
1. python manage.py startapp social


## Specific Technologies

- DocRaptor for html to pdf in Django - Razzi used it at a company. [stack overflow](https://stackoverflow.com/questions/22247595/generate-pdf-with-docraptor-in-django)



