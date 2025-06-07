# relational-database-service
This repository is used to document how I created my first rds database on aws and connected to it on my ec2 instance
# Creating A Database
I followed these steps to create a database with Amazon RDS
1. On the AWS Console , I searched RDS
2. Towards the left I clicked Databases
3. I clicked Create Database
4. I Selected “Standard Create” as the database creation method. 
5. I Chose the MySql Database Engine
6. I Selected the latest engine version
7. I chose a free-tier template
8. I inputted the name for the database on the DB Instance Identifier section
9. Under Credentials Settings
   a. I inputted admin as the Master Username
   b. I selected Self-Managed for Credentials Management
   c. I set the Master Password
14. Under Instance Configuration:
 a. I set the Instance type as db.t3.micro
16. Maintain the default settings for the Storage 
17. In VPC under connectivity , I selected my VPC
18. Under Public Access I selected “YES” 
19. Under Existing VPC security group, I selected my pre-exisiting vpc security group 
20. Under Availability Zones , I selected any of them
21. Leave other settings as default
22. Proceed by clicking “create database”

# In the Databases Section
1. I selected the database I just created by clicking on the database name
2.  scrolling down , you find an endpoint , copy and save this endpoint somewhere , alongside your database username and password

# Creating an EC2 instance for our RDS database connectivity
1. On the EC2 dashboard , click Launch Instance 
2. Input the name of the Instance
3. Select the Quick Start option and Select Amazon Linux as the AMI
4. For instance type select t2.micro
5. Select the Key Pair
6. Under Network Settings:
a. Click Edit 
b. Select the current VPC
c. Select a subnet 
d. Enable Auto-Assign Public IP
e. Select an existing security group that has inbound rules set for the right ports
7. Click Launch Instance.  

# Connecting to the EC2 instance
1. Connect to the instance via ssh
2. Run the command : sudo wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
3. Run sudo yum localinstall mysql57-community-release-el7-11.noarch.rpm
4. Run sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
5. Run sudo yum install mysql-community-server
6. Run sudo systemctl start mysqld.service
7. Run sudo systemctl enable mysqld.service
8. Run sudo systemctl status mysqld.service

# Connecting the RDS to the EC2 Instance
1. On the EC 2 instance enter the command : mysql -h [Endpoint] -P [Port] -u [Username] -p[Password]
