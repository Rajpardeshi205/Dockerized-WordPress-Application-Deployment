# Dockerized WordPress Application Deployment On AWS EC2

# **Project Introduction**

This Project Demonstrates How To Deploy A Complete WordPress Website Using Docker On An AWS EC2 Instance. The Application Uses Two Separate Docker Containers: One Container Runs **MySQL** As The WordPress Database, While The Second Container Runs **WordPress** As The Application Layer.

Docker Container Networking And Environment Variables Were Used To Connect WordPress With The MySQL Database. The WordPress Application Was Then Exposed Through A Dynamically Assigned Host Port And Accessed Using The EC2 Public IP Address.

This Project Provides Hands-On Experience With **Docker, AWS EC2, MySQL, WordPress, Container Networking, Environment Variables, And Linux Administration**.

# **Project Summary**

In This Project, I:

- Installed And Configured Docker On An AWS EC2 Instance.
- Added The `ec2-user` To The Docker Group.
- Pulled And Ran A MySQL Docker Container.
- Created A Dedicated WordPress Database Inside MySQL.
- Configured MySQL Using Environment Variables.
- Pulled And Ran The Official WordPress Docker Image.
- Connected WordPress With MySQL Using Database Environment Variables.
- Used Docker Container Linking To Establish Communication Between Containers.
- Exposed The WordPress Container Using A Dynamic Host Port.
- Accessed WordPress Through The EC2 Public IP.
- Completed The WordPress Installation And Accessed The WordPress Dashboard.

# Architecture

![Architecture.png](https://github.com/user-attachments/assets/5be110f1-2ff1-4fdf-8149-675126858780)

# Implementation Step

## 1. Update System & Install Docker

Update The EC2 Instance Packages And Install Docker.

```jsx
 sudo yum update
 sudo yum install docker -y
```

## 2. Start & Enable Docker

Start The Docker Service, Enable It To Start Automatically After Reboot, And Verify Its Status.

```jsx
sudo systemctl start docker
sudo systemctl enable docker
sudo systemctl status docker
```

## 3. Add User To Docker Group

Add The `ec2-user` To The Docker Group So Docker Commands Can Be Executed Without Using `sudo`.

```jsx
sudo gpasswd -a ec2-user docker
```

After Adding The User To The Docker Group, Log Out And Log Back In For The Group Membership To Take Effect.

## 4. Pull & Run MySQL Container

Run A MySQL Container To Create And Store The WordPress Database.

```jsx
docker run -d --name mydb -e MYSQL_ROOT_PASSWORD=root -e  MYSQL_DATABASE=wordpressdb mysql

docker run -> Creates And Starts A New Container
-d -> Runs The Container In Detached/Background Mode
--name mydb -> Gives The Container The Name mydb
-e MYSQL_ROOT_PASSWORD=root -> Sets The MySQL Root User Password To root
-e MYSQL_DATABASE=wordpressdb -> Automatically Creates A Database Named wordpressdb
mysql -> Uses The MySQL Docker Image
```

![image.png](https://github.com/user-attachments/assets/e0935a0a-ea21-49d2-9c58-69331875c5b2)

### Verify Docker Image

Check Whether The MySQL Image Has Been Downloaded Successfully.

```jsx
docker images
```

![image.png](https://github.com/user-attachments/assets/6afd072c-f07b-4698-aa07-7c8074daff52)

### Verify MySQL Container

Check Whether The MySQL Container Is Running.

```jsx
docker ps
```

![image.png](https://github.com/user-attachments/assets/91039d54-74fd-4a9e-80ee-419dfd41a7ba)

## 5. Pull & Run WordPress Container

Run The WordPress Container And Configure It To Connect To The MySQL Container.

```jsx
docker run -d -P --name wordpress -e WORDPRESS_DB_HOST=mydb -e WORDPRESS_DB_USER=root -e WORDPRESS_DB_PASSWORD=root -e WORDPRESS_DB_NAME=wordpressdb --link mydb:mysql wordpress

docker run -> Creates And Starts A New Container
-d -> Runs The Container In Background/Detached Mode
-P -> Automatically Maps The Container's Exposed Port To A Random Host Port
--name wordpress -> Names The Container wordpress
-e WORDPRESS_DB_HOST=mydb -> Tells WordPress That MySQL Is Available At Hostname mydb
-e WORDPRESS_DB_USER=root -> MySQL Username Is root
-e WORDPRESS_DB_PASSWORD=root ->MySQL Password Is root
-e WORDPRESS_DB_NAME=wordpressdb -> WordPress Uses The wordpressdb Database
--link mydb:mysql -> Links The WordPress Container To The mydb Container
wordpress -> Uses The Official WordPress Docker Image
```

### Verify WordPress Image

Check Whether The WordPress Image Has Been Downloaded.

```jsx
docker images
```

![image.png](https://github.com/user-attachments/assets/eab81509-92af-4c29-a301-972f00e45e0d)

### Verify WordPress Container

Check Whether The WordPress Container Is Running.

```jsx
docker ps
```

![image.png](https://github.com/user-attachments/assets/d9c9021c-35b7-402a-b1ee-94c0c72f8669)

## 6. Verify WordPress In Browser

The `-P` Option Automatically Publishes The Port Exposed By The WordPress Image To A Random Host Port.

Copy Public IP & Add 32768 Port

```jsx
54.83.182.63:32768
```

Make Sure The EC2 Security Group Allows Inbound TCP Traffic On Port `32768`. If You Recreate The Container, Docker May Assign A Different Port Because `-P` Automatically Selects The Host Port.

## 7. Complete WordPress Installation

After Opening The WordPress URL:

### **Select Language**

Select Your Preferred Language And Click **Continue**.

![image.png](https://github.com/user-attachments/assets/3b9cd1e3-76ec-4dd7-baf1-484ed0886640)

### **Configure WordPress**

Fill In The Required Information:

- Site Title
- Username
- Password
- Email Address

Then Click **Install WordPress**.

![image.png](https://github.com/user-attachments/assets/a6055806-525c-4955-bb09-e07478ab6741)

### Log In

After Installation Is Complete, Click **Log In.** 

![image.png](https://github.com/user-attachments/assets/f5872510-c5b8-454e-9f1c-2e0b67a7f397)

Enter The WordPress Username And Password.

![image.png](https://github.com/user-attachments/assets/3f8e13dc-6283-4d67-a178-127c937d100c)

### **WordPress Dashboard**

After Successful Authentication, The WordPress Dashboard Will Be Displayed.

![image.png](https://github.com/user-attachments/assets/bffcc711-aecd-4914-81b1-30408273e927)

# Summary

This Project Successfully Demonstrated The **Dockerized Deployment Of A WordPress Application Using MySQL On AWS EC2**. The WordPress Application And MySQL Database Were Deployed In Separate Docker Containers, With Environment Variables Used To Configure The Database Connection.

The Project Provided Hands-On Experience With **Docker Containerization, AWS EC2, MySQL Database Configuration, WordPress Deployment, Container Communication, Port Publishing, And Linux Administration**.

Through This Implementation, I Learned How To Deploy A Multi-Container Application, Connect An Application Container With A Database Container, Troubleshoot Container Connectivity, And Make A Dockerized WordPress Application Accessible Through An EC2 Public IP.

Overall, This Project Strengthened My Practical Understanding Of **Docker And AWS-Based Application Deployment** And Provided A Foundation For Learning More Advanced Container Technologies Such As **Docker Compose, Kubernetes, And Container Orchestration**.
