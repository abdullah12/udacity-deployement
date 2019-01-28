# Deploying Catalog App

This repo shows how to deploy a udacity catalog project 

## Create virtual Machine
and the note the ip and domain name  
ip : 35.170.33.100  
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

## create virtual enviroment on FlaskApp folder 
sudo pip install virtualenv  
sudo virtualenv env  
source venv/bin/activate  
sudo chmod -R 777 venv  

## install flask and the dependencies
sudo pip install flask request httplib2 oauth2client sqlalchemy psycopg2 sqlalchemy_utils  

## download the 





