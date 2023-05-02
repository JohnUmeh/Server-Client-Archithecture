# 5.Server-Client-Archithecture
Creating a Server and Client Web Architecture Using Mysql

# **SERVER-CLIENT ARCHITECTURE**
The client-server architecture refers to a system that hosts, delivers, and manages most of the resources and services that the client requests. In this model, all requests and services are delivered over a network, and it is also referred to as the networking computing model or client server network.

Client-server architecture, alternatively called a client-server model, is a network application that breaks down tasks and workloads between clients and servers that reside on the same system or are linked by a computer network.

Client-server architecture typically features multiple users’ workstations, PCs, or other devices, connected to a central server via an Internet connection or other network. The client sends a request for data, and the server accepts and accommodates the request, sending the data packets back to the user who needs them.

![Screenshot from 2023-03-06 12-49-21](https://user-images.githubusercontent.com/77943759/223102314-dbf86f46-5e13-4346-8ef9-ea300f50f95a.png)

In this project, we are going to demonstrate the server and client connection using two AWS ec2 instances, one as server, the other as client and connecting them over the public IP address rather than ssh

# **CREATE EC2 INSTANCES**

Create two linux based ec2 instances, name one as `Mysql-server` and the other as `Mysql-client`. Save their keypairs as .pem and connect to them on your terminal

![Instances](https://user-images.githubusercontent.com/77943759/223103257-dce76f71-dd08-465f-bbfe-ba2ce2317d6d.png)

On the mysql-server, install mysql server: Run

`sudo apt update`

`sudo apt upgrade`

`sudo apt install mysql-server`

![mysqlserver](https://user-images.githubusercontent.com/77943759/223104041-457b6ea0-8a74-4445-b20e-34f42b1da45d.png)

start mysql. Run 

`sudo mysql`

Create a user and set password

`CREATE USER 'username'@'host' IDENTIFIED WITH authentication_plugin BY 'password';`

![createuser](https://user-images.githubusercontent.com/77943759/223105508-fc3b0c9e-87fc-4a73-b60e-a86cec9babb0.png)


Create database. Run:

`CREATE DATABASE <DBname>`

![createdb](https://user-images.githubusercontent.com/77943759/223105925-fb52e94f-e67a-495b-b07f-f1146aedec4e.png)

In the image above, we created a database named conn_Test

Grant privileges to the created user on the database. Run

`GRANT ALL PRIVILEGES ON *.* TO 'username'@'host' WITH GRANT OPTION;`

![realprivilege](https://user-images.githubusercontent.com/77943759/223107075-da6af827-bd66-4db0-a464-2eb1915573e9.png)

Still on the mysql_server, we need to open the port for our server to be accessible

Open mysql_server instance and open port 3306

![port3306](https://user-images.githubusercontent.com/77943759/223107553-5d9000ae-3d8d-47e9-afbb-93391c2a9018.png)


We need to edit our server configuration file to allow access from remote hosts

`sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf`. Edit the bind-address part having 127.0.0.1 to 0.0.0.0

![bindaddress](https://user-images.githubusercontent.com/77943759/223108195-35109408-8987-4a5f-b85b-cdcb5a5e15d7.png)

## **mysql_client**

On the mysql_client instance, We will acess the mysql server through the ip address next

Run 

`sudo mysql -u username -h <public-ip-address> -p`

When promted for password, enter the password for the mysql user.

![loginmysql](https://user-images.githubusercontent.com/77943759/223109736-e14b1c9e-b805-4056-be43-d09a5190eaad.png)

This page shows the client connected successfully to mysql_server.

To confirm this, let us check the database created on mysql server. Run:

`mysql> show databases`

![showdb](https://user-images.githubusercontent.com/77943759/223110463-ab09715a-31e6-4e81-916e-d86d684f93b9.png)

The page above shows the database we created on msql_server. This confirms a successful connection from the mysql client to mysql server

DONE





