# RDS-LAB-1

create ec2 with az key pair ubuntu 
connect to server 
sudo su
sudo yum update
sudo yum install docker -y 
sudo systemctl start docker 
sudo systemctl status docker 

from docker hub pull
phpmyadmin 
give commnand
docker pull phpmyadmin
Usage with arbitrary server
docker run --name phpmyadmin -d -e PMA_ARBITRARY=1 -p 8080:80 phpmyadmin
docker ps 
docker images


Create database 
MySQL
Choose a database creation method

Full configuration
Templates

Sandbox
Availability and durability
Settings
MySQL Community
Engine version  
latest 
DB instance identifier: database-1
Credentials Settings
Master username
admin
Credentials management

Self managed
create password : admin12345
Additional credentials settings
Password authentication
Instance configuration
Burstable classes (includes t classes)
Instance type: db,t4 micro
Storage 
general purpose gp2
Allocated storage: 20
additional settings
Enable storage autoscaling
Maximum storage threshold : 1000
Compute resource
Connect to an EC2 compute resource
EC2 instance : select ec2 
EC2 instance

DB subnet group:choose existing
Existing DB subnet groups
select vpc
Public access
no
VPC security group (firewall)
choose existing 
Additional VPC security group   : seach ec2 sg name
Availability Zone: automatically selected 

rest default 
create 


opwn db 
Set up EC2 connection 

go to ec2 connection
sudo yum update -y
sudo yum install -y mariadb105-server
sudo systemctl start mariadb
sudo systemctl enable mariadb

RDS
CONNECTIVITTY 
Connect using
endpoint  : copy endpoint 
now in server give command
mysql -h database-1.c1q0e0awq6n7.ap-south-1.rds.amazonaws.com -u admin -p 
enter
now give password  
now you are inside sql container



insde ec2 securirty group 
give 
inbound rule
custom tcp --- port 8080--- anywhere ip ===save

copy ip paste:8080  in browser
login: english
serveer: copy endpoint url
username: admin
password

mysql -h database-1.c1q0e0awq6n7.ap-south-1.rds.amazonaws.com -u admin -p
SHOW DATABASES;
CREATE DATABASE db1;
SHOW DATABASES;

exit




















