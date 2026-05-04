# RDS-LAB-1

# Step 1

🚀 Create EC2 Linux Instance (Quick Steps)

Go to EC2 → Launch Instance

Enter Name

Select AMI

Amazon Linux / Ubuntu

Choose Instance Type

t2.micro

Create Key Pair
Download .pem

Select Network
Choose VPC
Select Subnet (this decides AZ)

Configure Security Group

Allow SSH (port 22 → My IP)

customTCP PORT 8080 ANYWHERE IP 

Click Launch

🔐 Connect
connect to server 
1. Connect to your EC2 instance
  
2. Switch to root user
```bash
sudo su
```
3. Update packages
yum update -y

4. Install Docker
yum install docker -y

5. Start Docker service
systemctl start docker

6. Check Docker status
systemctl status docker

7. Enable Docker on boot (important)
systemctl enable docker

8. Test Docker
docker run hello-world

# step 4

Steps to Run phpMyAdmin using Docker
1. Pull phpMyAdmin Image from Docker Hub
docker pull phpmyadmin

2. Verify Image Downloaded
docker images

3. Run phpMyAdmin Container
Usage with arbitrary server
docker run --name phpmyadmin -d -e PMA_ARBITRARY=1 -p 8080:80 phpmyadmin

What this does:

--name phpmyadmin → container name
-d → run in background
-e PMA_ARBITRARY=1 → connect to any MySQL server
-p 8080:80 → access via browser on port 8080

4. Check Running Containers
docker ps

5. Access phpMyAdmin in Browser
http://<EC2-PUBLIC-IP>:8080

⚠️ Important
Make sure port 8080 is open in your EC2 Security Group
You need a MySQL server to connect inside phpMyAdmin

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




















