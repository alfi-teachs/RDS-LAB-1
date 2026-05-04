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
```bash
yum update -y
```
5. Install Docker
```bash
yum install docker -y
```
7. Start Docker service
```bash
systemctl start docker
```
9. Check Docker status
```bash
systemctl status docker
```
11. Enable Docker on boot (important)
```bash
systemctl enable docker
```
13. Test Docker
```bash
docker run hello-world
```
# step 4

Steps to Run phpMyAdmin using Docker

1. Pull phpMyAdmin Image from Docker Hub

```bash
docker pull phpmyadmin
```

3. Verify Image Downloaded

```bash
docker images
```

4. Run phpMyAdmin Container
   
Usage with arbitrary server

```bash
docker run --name phpmyadmin -d -e PMA_ARBITRARY=1 -p 8080:80 phpmyadmin
```
What this does:

--name phpmyadmin → container name

-d → run in background

-e PMA_ARBITRARY=1 → connect to any MySQL server

-p 8080:80 → access via browser on port 8080

4. Check Running Containers

```bash
docker ps
```
6. Access phpMyAdmin in Browser

```bash
http://<EC2-PUBLIC-IP>:8080
```
⚠️ Important

Make sure port 8080 is open in your EC2 Security Group

You need a MySQL server to connect inside phpMyAdmin
--------------------------------------------------------
# 🔹 Step 1: Open RDS Service
Go to AWS Console
Search → RDS
Click Create database
# 🔹 Step 2: Choose Database Creation Method
Select: Standard create (Full configuration)
# 🔹 Step 3: Engine Options
Engine type: MySQL
Edition: MySQL Community
Version: Latest
# 🔹 Step 4: Templates
Select: Sandbox (for practice / lab)
# 🔹 Step 5: Settings
DB instance identifier: database-1
Master username: admin
Password: admin12345
Confirm password: admin12345
Credentials management: Self-managed
# 🔹 Step 6: Instance Configuration
Instance class: Burstable (t class)
Instance type: db.t4g.micro (small and cost-effective)
# 🔹 Step 7: Storage
Storage type: General Purpose (gp2)
Allocated storage: 20 GB
Enable storage autoscaling: ✅ Yes
Maximum storage threshold: 1000 GB
# 🔹 Step 8: Connectivity
Connect to EC2 compute resource: ✅ Yes
Select EC2 instance: (choose your EC2)
# 🔹 Step 9: Network Settings
DB subnet group: Choose existing
Select your VPC subnet group
Public access: ❌ No (private DB for security)
VPC security group:
Select: Choose existing
Add security group: (same SG as EC2 or allow MySQL port 3306)
Availability Zone: Automatic
# 🔹 Step 10: Additional Settings
Keep everything default
# 🔹 Step 11: Create Database
Click Create database
# 🔹 Important After Creation

Once DB is ready:

Go to RDS → Databases

Copy Endpoint

Connect from EC2:
```bash
mysql -h <endpoint> -u admin -p
```

Enter password:
🔹 Step 1: Open RDS Service
Go to AWS Console
Search → RDS
Click Create database
🔹 Step 2: Choose Database Creation Method
Select: Standard create (Full configuration)
🔹 Step 3: Engine Options
Engine type: MySQL
Edition: MySQL Community
Version: Latest
🔹 Step 4: Templates
Select: Sandbox (for practice / lab)
🔹 Step 5: Settings
DB instance identifier: database-1
Master username: admin
Password: admin12345
Confirm password: admin12345
Credentials management: Self-managed
🔹 Step 6: Instance Configuration
Instance class: Burstable (t class)
Instance type: db.t4g.micro (small and cost-effective)
🔹 Step 7: Storage
Storage type: General Purpose (gp2)
Allocated storage: 20 GB
Enable storage autoscaling: ✅ Yes
Maximum storage threshold: 1000 GB
🔹 Step 8: Connectivity
Connect to EC2 compute resource: ✅ Yes
Select EC2 instance: (choose your EC2)
🔹 Step 9: Network Settings
DB subnet group: Choose existing
Select your VPC subnet group
Public access: ❌ No (private DB for security)
VPC security group:
Select: Choose existing
Add security group: (same SG as EC2 or allow MySQL port 3306)
Availability Zone: Automatic
🔹 Step 10: Additional Settings
Keep everything default
🔹 Step 11: Create Database
Click Create database
🔹 Important After Creation

Once DB is ready:

Go to RDS → Databases
Copy Endpoint
Connect from EC2:
mysql -h <endpoint> -u admin -p


Enter password:
```bash
admin12345
admin12345
```

✅ Step 1: Ensure RDS is Created
RDS MySQL instance should be Available
Copy the RDS Endpoint
✅ Step 2: Configure Security Group (Important)
Go to RDS → Security Group
Add inbound rule:
Type: MySQL/Aurora
Port: 3306
Source: EC2 Security Group
✅ Step 3: Connect to EC2
Open EC2 terminal (SSH)
✅ Step 4: Install MySQL Client (NOT Server)
sudo yum update -y
sudo yum install -y mariadb

✅ Step 5: Connect to RDS Database
mysql -h <RDS-endpoint> -u admin -p

Enter password:
admin12345

🔹 Final Architecture Understanding
RDS → Database Server
EC2 → Client machine

🔥 Quick Check if Connection Fails
RDS status = Available
Correct endpoint used
Port 3306 open in Security Group
EC2 and RDS in same VPC


Ensure RDS Security Group

In RDS Security Group → Inbound Rules:

Type: MySQL/Aurora
Port: 3306
Source: EC2 Security Group

Connect to RDS Database
mysql -h <RDS-endpoint> -u admin -p

Enter password:
admin12345


Step 5: Login Details
Language: English
Server: RDS Endpoint (paste it)
Username: admin
Password: admin12345



mysql -h database-1.c1q0e0awq6n7.ap-south-1.rds.amazonaws.com -u admin -p
SHOW DATABASES;
CREATE DATABASE db1;
SHOW DATABASES;

exit




















