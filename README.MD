# Deploying Catalog App

This repo shows how to deploy a udacity catalog project 

## Create virtual Machine
and the note the ip and domain name  
ip : 3.89.198.13  
domain name :progtut.site  

connect to the machine using ssh  

## Add user and add it to the sudo group
sudo adduser grader  
sudo usermod -aG sudo grader  

## generate ssh keys and paste the public key to the server
ssh-kegen
copy the content of public key
log into the server 
swithc to gradee account
create a file authorized_keys in ~/.ssh folder
pase the content of pubilc key into the authorized_keys flile

## Update the system
sudo apt update  
sudo apt upgrade  


## change ssh default port
configure ssh to port 2200 on the file /etc/ssh/sshd_config  
sudo service sshd restart  

## configure the firewall

sudo ufw allow 2200/tcp  
sudo ufw allow 80  
suod ufw allow 123/udp  
udo ufw enable  

## setting the timezone to UTC
sudo dpkg-reconfigure tzdata  


## disable ssh login for root user

## install apache and mod_wsgi
sudo apt install apache2  
sudo apt install libapache2-mod-wsgi python-dev  
sudo a2enmod wsgi  

## Install postgresql and create the database
sudo apt-get install libpq-dev python-dev  
sudo apt-get install postgresql postgresql-contrib  
sudo su - postgres  
psql  
CREATE USER catalog WITH PASSWORD 'password';  
ALTER USER catalog CREATEDB;  
CREATE DATABASE catalog WITH OWNER catalog;  
\c catalog  
REVOKE ALL ON SCHEMA public FROM public;  
GRANT ALL ON SCHEMA public TO catalog;  
\q  
exit  

## create virtual enviroment on FlaskApp folder 
sudo pip install virtualenv  
sudo virtualenv env  
source venv/bin/activate  
sudo chmod -R 777 venv  

## install flask and the dependencies
sudo pip install flask request httplib2 oauth2client sqlalchemy psycopg2 sqlalchemy_utils  

## clone the app 
create folder FlaskApp in /var/www/
inside FlaskApp create file catalog.wsgi with this content
```
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0, "/var/www/FlaskApp/")

from FlaskApp import app as application
application.secret_key = 'supersecretkey'
```
insdie the FlaskApp create another FlaskApp and change to the created folder  

git clone https://github.com/abdullah12/catalog-project.git .  

change app.py to __init__.py  
change the path of client_secrets.json inside __init__.py  

## configure apache virtual host 
```
<VirtualHost *:80>
    ServerName 3.89.198.13
    ServerAlias http://3.89.198.13.xip.io
    ServerAdmin admin@35.167.27.204
    WSGIDaemonProcess catalog python-path=/var/www/FlaskApp:/var/www/FlaskApp/venv/lib/python2.7/site-packages
    WSGIProcessGroup catalog
    WSGIScriptAlias / /var/www/FlaskApp/catalog.wsgi
    <Directory /var/www/FlaskApp/FlaskApp/>
        Order allow,deny
        Allow from all
    </Directory>
    Alias /static /var/www/FlaskApp/FlaskApp/static
    <Directory /var/www/FlaskApp/FlaskApp/static/>
        Order allow,deny
        Allow from all
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/error.log
    LogLevel warn
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```







