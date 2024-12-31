# Installing MariaDB, Setting Password, and Importing Database on Ubuntu Linux

This guide will walk you through the process of installing MariaDB on Ubuntu Linux, setting a password, and importing a database from a SQL file. MariaDB is a popular open-source relational database management system, and it's commonly used in web development environments.

## Setup MariaDB and Import MySQL

Before installing any new software, it's essential to update the package lists to ensure you're getting the latest versions available.

```bash
sudo apt update
sudo apt install mariadb-server
sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo mysql_secure_installation
sudo mysql -u root -p
```
# Go inside into databse 
```bash
 mysql -h <RDS-ENDPOINT> -u admin -p
```
# GO INside the databse run follwing comands
```bash
CREATE DATABASE springbackend;
GRANT ALL PRIVILEGES ON springbackend.* TO 'username'@'localhost' IDENTIFIED BY 'your_password';
```

### Exit form databse and run following command Import Database from SQL File
```bash
sudo mysql -h <RDS-ENDPOINT> -u username -p springbackend < springbackend.sql
```
```bash
sudo mysql -u root -p
```
```sql
show databases;
show tables;
select * from tbl_workers;
```

# Above step u can do manually for creating db or you can create RDS on aws console, and integrate your RDS to EC2. 
# Step for Crating RDS 
Select Remotely public access yes

Self manage provide password for rds and username 

Do not Select ec2 

Connect to RDS to ec2  using CLI.  

click on create RDS

```bash
mysql -h database-1.cxacw26ek87r.ap-south-1.rds.amazonaws.com -u admin -p
```
after go inside the mysql-db, then use this readme files commands to create table and all, All commands mentioned above.


![image](https://github.com/user-attachments/assets/fa1062ed-3a0f-4c23-8c0b-a499425d9202)




# All steps of Project

step 1: 
Create a DB using above steps mentioned in same readme file.
Connect db to backend Go inside spring backend folder and check steps

step 2: 
Go in spring-backend folder Readme file follow all steps to create a backend continer.

step 3 :
Go in angular-frontend folder readme file and follow all steps to run frontend.





