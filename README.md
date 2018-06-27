# django-rest-api-test-docker
Using Django REST-API framework with Postgres in docker container and frontend (vue.js) in other container,

## 1) Create new django project and connect to Postgres that works in Docker (it is a good choice for development)

1. Create new Django project (i recommend creating a folder with a virtual environment not in the project folder)
1. Install psycopg2 (use **`pip install psycopg2`**)
1. Change DB settings in **`settings.py`**:
   ```
   DATABASES = {
      'default': {
      	   'ENGINE': 'django.db.backends.postgresql_psycopg2',
        	   'NAME': 'django_rest_api',
        	   'USER': 'admin',
        	   'PASSWORD': 'password',
        	   'HOST': 'localhost',
        	   'PORT': '5432',
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
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: password
  ```
5. Run docker: `docker-compose up`. After this lets go create user in our DB:
    * run bash: **`$:/# docker exec -i -t postgres-docker_postgres9_1 /bin/bash`**
    * open your db console: **`$:/# psql -U admin django_rest_api;"`**
    * check all table: **`django_rest_api=# \dt`**, (it will return `No relations found.`)
    * go back to django project and migrate default data: **`(venv) path_to_manage.py\src>python manage.py migrate`**
    * check all table again: **`django_rest_api=# \dt`** and it will return:
      ```
                     List of relations
       Schema |            Name            | Type  | Owner
      --------+----------------------------+-------+-------
       public | auth_group                 | table | admin
       public | auth_group_permissions     | table | admin
       public | auth_permission            | table | admin
       public | auth_user                  | table | admin
       public | auth_user_groups           | table | admin
       public | auth_user_user_permissions | table | admin
       public | django_admin_log           | table | admin
       public | django_content_type        | table | admin
       public | django_migrations          | table | admin
       public | django_session             | table | admin
      (10 rows)
      ```
    * Congratulations!
    
    
