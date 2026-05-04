# RDS-LAB-1

# Step 1

Go to AWS Console → EC2 → Launch Instance

Configure:

Name: any (e.g., rds-client)

AMI: Amazon Linux 2

Instance Type: t2.micro

Key Pair: Create and download .pem

Network Settings:

Select your VPC
Select Subnet (AZ)

Security Group (Very Important):
Add inbound rules:

| type        | port         | source  |
|-------------|--------------|---------|
| SSH         | 22           | MY IP   |
| CUSTOM TCP  | 8080         |  Anywhere (0.0.0.0/0) |


Click Launch

#🔹 Step 2: Connect to EC2
```bash
ssh -i key.pem ec2-user@<EC2-PUBLIC-IP>
```
  
2. Switch to root user
```bash
sudo su
```
3. Update packages
```bash
yum update -y
```
# step 3
1. Install Docker
```bash
yum install docker -y
```
2. Start Docker service
```bash
systemctl start docker
```
3. Check Docker status
```bash
systemctl status docker
```
4. Enable Docker on boot (important)
```bash
systemctl enable docker
```
5. Test Docker
```bash
docker run hello-world
```
# step 4

Steps to Run phpMyAdmin using Docker

1. Pull phpMyAdmin Image from Docker Hub

```bash
docker pull phpmyadmin/phpmyadmin
```

2. Verify Image Downloaded

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
# ⚠️ Important

Make sure port 8080 is open in your EC2 Security Group

You need a MySQL server to connect inside phpMyAdmin
--------------------------------------------------------
Create RDS MySQL Database

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
```bash
admin12345
```
---------------------------------------------------------------------------

# ✅ Step 1: Ensure RDS is Ready
RDS MySQL instance status: Available
Copy the RDS Endpoint

# ✅ Step 2: Configure Security Groups

🔸 RDS Security Group (Important)

Go to RDS → Security Group → Inbound Rules

Add:
Type: MySQL/Aurora
Port: 3306
Source: EC2 Security Group

✔ This allows EC2 to talk to RDS

🔸 EC2 Security Group

Default outbound is allowed ✅ (no change needed)

(Optional — only if using browser tools later)

Add:
Type: Custom TCP
Port: 8080
Source: Anywhere (0.0.0.0/0)

# ✅ Step 3: Connect to EC2

SSH into EC2:

ssh -i key.pem ec2-user@<EC2-Public-IP>

# ✅ Step 4: Install MySQL Client (Only)
```bash
sudo yum update -y
```
```bash
sudo yum install -y mariadb
```
✔ Installs MySQL client to connect RDS

# ✅ Step 5: Connect to RDS Database
```bash
mysql -h database-1.c1q0e0awq6n7.ap-south-1.rds.amazonaws.com -u admin -p
```

Enter password:
```bash
admin12345
```
# ✅ Step 6: Run MySQL Commands
```bash
SHOW DATABASES;

CREATE DATABASE db1;

SHOW DATABASES;
```
# ✅ Step 7: Exit MySQL
```bash
exit;
```
#  Step 8: Browser Login (phpMyAdmin)

If configured:

URL:

```bash
http://<EC2-Public-IP>:8080/phpmyadmin
```
Login:

Language: English

Server: RDS Endpoint

Username: admin

Password: admin12345


# 🔹 Final Architecture

RDS → MySQL Database Server

EC2 → Client machine (connects to RDS)

# 🔥 Troubleshooting Checklist

RDS status = Available

Correct endpoint used

Port 3306 open in RDS SG

EC2 & RDS in same VPC

Username/password correct





















