Docker django web server
=========

This project allows you to install a web server for Django. It contains nginx, app, postgre containers.

Preparations
------------

An appropriately prepared container in which the files will be replaced is required.
For the project to work properly, you must:

1. generate ssl certificates and copy them to the SSL directory to the files that are currently empty.

2. edit the settings.py file in the app directory:

    - INSTALLED_APPS - add the django project applications
    - ROOT_URLCONF - replace the word project with the name of your project
    - WSGI_APPLICATION - replace the word project
    - add variables according to your needs and dependencies.

3. copy the django project to the app directory and replace setting.py with the one edited from the point above.
4. create .env and .env.db files in the project:

- the .env file should contain the following variables:

    ~~~bash
    SQL_ENGINE=django.db.backends.postgresql
    SQL_DATABASE=database_name
    SQL_USER=database_admin_name
    SQL_PASSWORD=database_password
    SQL_HOST=db
    SQL_PORT=5432
    DATABASE=postgres
    VIRTUAL_HOST=localhost
    VIRTUAL_PORT=8000
    LETSENCRYPT_HOST=localhost

    DEBUG=False
    SECRET_KEY=generated_secret_key
    DJANGO_ALLOWED_HOSTS="server_IP,localhost"
    SESSION_COOKIE_SECURE=True
    CSRF_COOKIE_SECURE=True
    CSRF_COOKIE_AGE=3153600
    CSRF_TRUSTED_ORIGINS="https://server_IP,https://localhost"
    SECURE_HSTS_SECONDS=3153600
    SECURE_HSTS_INCLUDE_SUBDOMAINS=True
    SECURE_HSTS_PRELOAD=True

    CSP_DEFAULT_SRC="'self'"
    CSP_SCRIPT_SRC="'self', reqired_links_with_scripts"
    CSP_STYLE_SRC="'self', required_links_with_styles"
    CSP_SCRIPT_SRC_ELEM="'self', required_links_with_scripts"
    CSP_FONT_SRC="'self', required_links_with_fonts"
    CSP_IMG_SRC="'self','data:'"
    CSP_CONNECT_SRC="'self'"
    CSP_INCLUDE_NONCE_IN=script-src,font-src,script-src-elem
    CSP_INCLUDE_SUBDOMAINS=True
    ~~~

- the .env.db file should contain the following variables:

    ~~~bash
    POSTGRES_USER=idea_art_db_admin
    POSTGRES_PASSWORD=qjkxQJKX
    POSTGRES_DB=idea_art_db 
    ~~~

Files
------------

.env and .env.db these files should be in the django project directory ./app/

- .env - change all variables like database name, sql username, password and others for your needs. Examples are given below.
- .env.db - the data provided should be the same as in .env

Veriables
------------

1. DJANGO_ALLOWED_HOSTS="server_IP,localhost"

    example:

    ~~~bash
    DJANGO_ALLOWED_HOSTS="192.168.88.246,localhost"
    ~~~

2. CSRF_TRUSTED_ORIGINS="https://server_IP,https://localhost"

    example:

    ~~~bash
    CSRF_TRUSTED_ORIGINS="https://192.168.88.246,https://localhost"
    ~~~

3. CSP_SCRIPT_SRC="'self', reqired_links_with_scripts"

    example:

    ~~~bash
    CSP_SCRIPT_SRC="'self',https://cdn.jsdelivr.net,https://*.googleapis.com,https://ajax.googleapis.com"
    ~~~

4. CSP_STYLE_SRC="'self', required_links_with_styles"

    example:

    ~~~bash
    CSP_STYLE_SRC="'self',https://*.googleapis.com,'nonces'"
    ~~~

5. CSP_SCRIPT_SRC_ELEM="'self', required_links_with_scripts"

    example:

    ~~~bash
    CSP_SCRIPT_SRC_ELEM="'self',https://cdn.jsdelivr.net,https://*.googleapis.com"
    ~~~

6. CSP_FONT_SRC="'self', required_links_with_fonts"

    example:

    ~~~bash
    CSP_FONT_SRC="'self',https://fonts.gstatic.com,https://*.googleapis.com"
    ~~~

Usage
------------

If everything has been changed correctly, after running the commands below in the directory where docker-compose is located in your browser at the address given in .env you should see the running django project. Remember that we are running the project in https mode, http is forbidden, so the address should also be entered in this way.

~~~bash
docker compose up -d --build 
docker compose web exec python manage.py collectstatic
docker compose web exec python manage.py migrate
~~~

Other links
------------

1. Automatic server installation: <https://github.com/ArkadiuszStanislawLega/ansible-start-server>
2. Creating a backup: <https://github.com/ArkadiuszStanislawLega/ansible-make-backup>
3. Sending a backup: <https://github.com/ArkadiuszStanislawLega/ansible-push-backup>

License
-------

BSD
