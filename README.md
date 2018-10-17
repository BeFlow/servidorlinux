# servidorlinux
Projeto Servidor Linux do nanodegree Full Stack da Udacity.

# Configurando servidores Linux Project

This project is part of Full Stack Nanodegree

> Julio Cesar Oliveira da Silva

## Introduction

The proposal  of this project is the installation of a Linux distribution on a virtual machine and prepare it to host your web application.

## Instructions

IP privado: ( is not required here. )
IP público: 18.191.212.149

## Porta
Porta ssh: 2200

## URL Completa
http://18.191.212.149/

# Tasks Summary
## Create a new User named grader
1. sudo adduser grader
2. type in grader ALL=(ALL:ALL) ALL, save and quit

## Set ssh login using keys
1. ssh-keygen in local machine for generate keys 
2. deploy public key on developement enviroment

On virtual machine follow commands below:

$ su - grader
$ mkdir .ssh
$ touch .ssh/authorized_keys
$ vim .ssh/authorized_keys
Copy the public key generated on your local machine to this file and save

$ chmod 700 .ssh
$ chmod 644 .ssh/authorized_keys

3. ssh restart for reload SSH

## Update all currently installed packages

1. sudo apt-get update
2. sudo apt-get upgrade

## Change the SSH port from 22 to 2200

1. Use sudo nano  /etc/ssh/sshd_config and then change Port 22 to Port 2200 
2. save & quit. ( ctrl+x + yes + enter)
3. Reload SSH using sudo service ssh restart

## Configure Firewall (UFW)

1. sudo ufw default allow outgoing
2. sudo ufw default deny incoming
3. sudo ufw allow 2200/tcp
4. sudo ufw allow 80/tcp
5. sudo ufw allow 123/udp
6. sudo ufw enable 

## Configure the local timezone to UTC

Configure the time zone sudo dpkg-reconfigure tzdata

## Install and configure Apache to serve a Python mod_wsgi application

1. Install Apache sudo apt-get install apache2
2. Install mod_wsgi sudo apt-get install python-setuptools libapache2-mod-wsgi
3. Restart Apache sudo service apache2 restart

## Install and configure PostgreSQL

1. sudo apt-get install postgresql
2. login with: sudo su - postgres
3. create a new database
4. set a password
5. give permission and privileges for new database
6. quit qith: postgres=# \q
7. exit

## Install git, clone and setup App project

1. Install git, clone and setup your Catalog App project
2. Use cd /var/www to move to the /var/www directory
3. sudo mkdir AppOwn
4. cd AppOwn
5. Clone the Catalog App to the virtual machine with git clone command

## Configure and Enable a New Virtual Host

1. Create AppOwn.conf to edit: sudo nano /etc/apache2/sites-available/AppOwn.conf

2. Add the following lines of code to the file to configure the virtual host.

<VirtualHost *:80>
	ServerName 18.191.212.149
	ServerAdmin julioamadobr@gmail.com
	WSGIScriptAlias / /var/www/AppOwn/appown.wsgi
	<Directory /var/www/AppOwn/AppOwn/>
		Order allow,deny
		Allow from all
	</Directory>
	Alias /static /var/www/AppOwn/AppOwn/static
	<Directory /var/www/AppOwn/AppOwn/static/>
		Order allow,deny
		Allow from all
	</Directory>
	ErrorLog ${APACHE_LOG_DIR}/error.log
	LogLevel warn
	CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

3. Enable with: sudo a2ensite AppOwn

## Create the .wsgi File

1. Create the .wsgi Fil with commands:

1.1 cd /var/www/AppOwn
1.2 sudo nano appown.wsgi 


2. Add the following lines of code to the appown.wsgi file:

#!/usr/bin/python
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0,"/var/www/AppOwn/")

from AppOwn import app as application
application.secret_key = 'secret key'

## Restart Apache

sudo service apache2 restart


# REFERENCE

Udacity course: Configuring Linux Web Servers 
https://br.udacity.com/course/configuring-linux-web-servers--ud299



