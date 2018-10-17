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

# Tasks
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
