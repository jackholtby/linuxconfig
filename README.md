# Linux Server Configuration - Udacity Project
Author: Jack Holtby

## What is this?
A web server to serve the item catalogue which can be found [here](https://github.com/jackholtby/catalogue).

The web server runs at:

IP address: http://13.250.54.196

URL: http://13.250.54.196/category

SSH Port: 2200

## Software requirements:
- apache2
- libapache2-mod-wsgi
- postgresql
- git
- sqlite3

#### Python modules installed
- pip
- Flask
- sqlalchemy
- oauth2client
- sqlalchemy.orm
- requests
- virtualenv
- psycopg2
- pipreqs
- httplib2
- google_api_python_client
- ipaddr

## Configurations
Installed relevant software. See above.

Activated the wsgi mod.

Created /var/www/catalogue/catalogue directories.

Created /var/www/catalogue/catalogue/static directory.

Downloaded item catalogue project into /var/www/catalogue/catalogue
and renamed project.py to \__init__.py.

Changed the app.run() line in \__init__.py so that it didn't name the IP address or port.

Installed necessary python modules. See above.

Created the virtual environment called udacity. Installed necessary python modules inside it.

#### Apache config

Setup /etc/apache2/sites-available/catalogue.conf with the following:

```
<VirtualHost *:80>
		ServerName 13.250.54.196
		ServerAdmin admin@54.254.156.84
		WSGIScriptAlias / /var/www/catalogue/catalogue.wsgi
		<Directory /var/www/catalogue/catalogue/>
			Order allow,deny
			Allow from all
		</Directory>
		Alias /static /var/www/catalogue/catalogue/static
		<Directory /var/www/catalogue/catalogue/static/>
			Order allow,deny
			Allow from all
		</Directory>
		ErrorLog ${APACHE_LOG_DIR}/error.log
		LogLevel warn
		CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

And then activated it with:

`sudo a2ensite catalogue`

.wsgi file setup:

In /var/www/catalogue/catalogue.wsgi:

```
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0,"/var/www/catalogue/")

from catalogue import app as application
application.secret_key = 'Add your secret key'
```

Then according to one tutorial, I was supposed to be done. Eheh. As if.

## Database setup
Installed postgresql.

Created a postgresql account and database both called catalogue.
Stopped public access to it.

Changed the database create_engine string to connect to the postgres database.
So that's in the database_setup.py, populate_database.py and \__init__.py files.

## Google server fix up
Added IP javascript origins for login and gconnect to the google credentials for the web app.
Added the proper domain name. Unfortunately google blocks it so.. have fun logging in.

## Acknowledgements
[Flask Deployment Tutorial on Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps)

[Linux Server Project by bad2thuhbone](https://github.com/bad2thuhbone/Linux-Server-Project-6)

[Converting to PostgreSQL from other database](https://wiki.postgresql.org/wiki/Converting_from_other_Databases_to_PostgreSQL)

Thus Endeth my project.
