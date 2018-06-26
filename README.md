# django-rest-api-test-docker
Using Django REST-API framework with Postgres in docker container and frontend (vue.js) in other container,

## 1) Create new django project and connect to Postgres that works in Docker (it is a good choice for development)

1. Create new Django project (i recommend creating a folder with a virtual environment not in the project folder)
1. Install psycopg2 (use `pip install psycopg2`)
1. Change DB settings in `settings.py`:
   ```
   DATABASES = {
   		'default': {
      		'ENGINE': 'django.db.backends.postgresql_psycopg2',
        	'NAME': 'django_rest_api',
        	'USER': 'user',
        	'PASSWORD': 'password',
        	'HOST': 'localhost',
        	'PORT': '',
      }
   }

1. Create `docker-compose.yml`:
  ```
  version: '3'

  services:
    postgres9:
      image: postgres:9.6
      ports:
        - 5432:5432
        
    environment:
      POSTGRES_DB: django_rest_api
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
  ```
5. Run docker: `docker-compose up`. After this lets go create user in our DB:
    * run bash: `docker exec -i -t postgres-docker_postgres9_1 /bin/bash`
