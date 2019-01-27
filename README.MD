# Deploying Catalog App

This repo shows how to deploy a udacity catalog project 

## Create virtual Machine
and the note the ip and domain name  
ip : 35.170.33.100  
connect to the machine using ssh  

## Add user and add it to the sudo group
sudo adduser grader  
sudo usermod -aG sudo grader  

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

## install apache
sudo apt install apache2




