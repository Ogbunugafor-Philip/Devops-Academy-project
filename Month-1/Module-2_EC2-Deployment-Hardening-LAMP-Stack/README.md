# EC2 Deployment, Hardening & LAMP Stack Setup

## Introduction

This project introduces students to real-world cloud computing by provisioning and managing an EC2 instance on AWS. It extends the Linux fundamentals from Project 1 into a practical cloud environment, showing how the same concepts of users, groups, and permissions apply when working on a live server. Students will learn how to securely connect to an instance using SSH keys, apply best practices in server hardening to reduce security risks, and configure the system for operational readiness. The project culminates with the installation of a complete LAMP stack (Linux, Apache, MySQL, PHP), giving learners first-hand experience in preparing a server to host dynamic web applications. This exercise not only strengthens their Linux administration skills but also builds confidence in managing cloud-based infrastructure, which is essential for modern DevOps roles.

## Statement of Problem
Organizations moving workloads to the cloud require engineers who can provision servers, secure them against unauthorized access, and prepare them for application deployment. Without standardized practices, servers are left vulnerable to attacks, poorly documented, and unstable. This project addresses the challenge of establishing a secure, operational, and ready-to-use server environment.

## Objectives
- To launch and configure a cloud server using AWS EC2.
- To establish secure remote access with SSH key pairs.
- To apply server hardening best practices (users, groups, firewall, updates).
- To install and verify a LAMP stack for web application hosting.

## Project Steps
i.	Launch an EC2 instance in AWS

ii.	Apply security hardening and configure SSH access and connect to the instance.

iii.	Install and configure a LAMP stack and verify services with systemctl and confirm deployment readiness.

## Project Implementation

### Step 1: Launch an EC2 instance in AWS
Amazon EC2 (Elastic Compute Cloud) is a virtual server that runs in the AWS cloud. It provides scalable computing resources without the need to buy or maintain physical hardware. In this step, we launch an EC2 instance to act as our training server, where we’ll practice secure connections, user management, and application hosting. This lays the foundation for all subsequent DevOps activities in the cloud.


- Sign in to AWS and Launch it
  <img width="975" height="398" alt="image" src="https://github.com/user-attachments/assets/f5c4a70e-67eb-4e7c-a2b5-2d63b78854d7" />

- Go to EC2 → Instances → Launch instances.
  <img width="975" height="326" alt="image" src="https://github.com/user-attachments/assets/8f1a8c11-239f-4ad7-9a9f-a5a55985ff74" />

 - Name: Lamp_Stack
   <img width="975" height="390" alt="image" src="https://github.com/user-attachments/assets/fc0cdfa0-d2fc-4e87-beb6-e63f8e06279f" />

 - AMI (OS): Ubuntu Server 24.04 LTS (recommended for our commands).
   <img width="975" height="401" alt="image" src="https://github.com/user-attachments/assets/79db1656-9a2a-4eaf-b659-2cb45f67835b" />

- Instance type: t3.micro (Free Tier eligible).
  <img width="975" height="168" alt="image" src="https://github.com/user-attachments/assets/b5cf95f2-1321-47d4-adcd-a0c5a7c9c2ce" />


- Key pair: Create new key pair → Type: RSA → Format: .pem → Download it (keep safe).
  <img width="975" height="169" alt="image" src="https://github.com/user-attachments/assets/4bdfc6ac-26dc-4fb1-be2f-7f5b9456d1df" />
 

- Click Launch instance
  <img width="975" height="280" alt="image" src="https://github.com/user-attachments/assets/d6cd865c-ad92-4d75-9a3c-3a2a738d3771" />

 
### Step 2: Apply security hardening and configure SSH access and connect to the instance
Secure Shell (SSH) is the standard protocol used to log into servers remotely and manage them safely over the network. Configuring SSH access ensures only authorized users with valid key pairs can connect, reducing the risk of brute-force password attacks. In this step, we’ll set up our SSH keys, connect to the EC2 instance, and verify that we have secure administrative access to the server.

Before we SSH, we would need to open a few ports to be accessed only by our IP address

- 22 (SSH): Required for remote login and management.
- 80 (HTTP): Required for Apache/PHP to serve web content.
- 3306 (MySQL): Required for database access (keep closed to the public, use only if remote DB access is necessary).
- 
To open these ports, follow the process

- Find Your Instance
    - Select the EC2 instance you launched.
      <img width="917" height="211" alt="image" src="https://github.com/user-attachments/assets/edaf189e-c6f0-4df9-89e0-91e88be27631" />

   - Scroll down to the Security tab.
     <img width="909" height="237" alt="image" src="https://github.com/user-attachments/assets/f3b7529e-23f1-4457-9185-d08f1887cdad" />


  - Click the Security Group attached to the instance
    <img width="906" height="267" alt="image" src="https://github.com/user-attachments/assets/de32ea03-083c-426b-b35d-8d7ee6f0dd28" />


- Edit Inbound Rules
    - Under Inbound rules, click Edit inbound rules.
      <img width="923" height="217" alt="image" src="https://github.com/user-attachments/assets/35f83a3b-e448-466c-862a-b57b4ec3eaf8" />

 
   - Click Add Rule.
     <img width="909" height="227" alt="image" src="https://github.com/user-attachments/assets/a77ee25e-d1de-4978-b91f-be6be3005326" />

     
 

- Select the Port / Protocol
    - For SSH → choose SSH (22).
    - For Apache HTTP → choose HTTP (80).
    - For MySQL → choose MySQL/Aurora (3306).

- Set the Source
    - SSH (22): Select My IP (so only your computer can connect).
    - HTTP (80): Select Anywhere (0.0.0.0/0) to allow public web access.
    - MySQL (3306): Only if needed → choose My IP (or a specific private IP of another server).
      <img width="940" height="267" alt="image" src="https://github.com/user-attachments/assets/66b45ab4-ddf9-4e3c-b7c3-7b252e7437e8" />

 
Click Save rules to apply changes immediately.

Now, let us SSH into our EC2 instance from our remote computer


- Open your git-bash and run this command
```bash
cd Downloads
 ```
<img width="933" height="164" alt="image" src="https://github.com/user-attachments/assets/db68fbbb-ad8b-444b-9638-efeefdf52f8d" />


- Then run this with the Public IP of your instance to ssh into it
```bash
ssh -i "C:\Users\<YOU>\Downloads\mykey.pem" ec2-user@<PUBLIC_IP>
 ```
<img width="975" height="327" alt="image" src="https://github.com/user-attachments/assets/83ef047e-c2fa-43ca-a293-f50ac038ffca" />


### Step 3: Install and configure a LAMP stack and verify services with systemctl and confirm deployment readiness

In this step, we are going to install the LAMP stack — Linux, Apache, MySQL, and PHP.
The LAMP stack is one of the most important setups in web development and server administration. Apache is the web server that shows our pages to users, MySQL is the database that stores and organizes data, and PHP connects everything to build dynamic websites and applications. By finishing this step, our server will be fully ready to host a real-world website.

- Update the package list. Always update before installing new software. Run;
```bash
sudo apt update
```
<img width="975" height="326" alt="image" src="https://github.com/user-attachments/assets/92cb8f36-a916-4287-8e1e-e9a98c650891" />

 
- Install Apache Web Server. Apache will serve web pages to visitors. Run;
```bash
sudo apt install apache2 -y
```
<img width="975" height="338" alt="image" src="https://github.com/user-attachments/assets/829f1e6e-d9f8-48e9-8dfe-73d92966fbaf" />
 

- Install MySQL (Database Server). We use MySQL to store and manage website/application data. Run;
```bash
sudo apt install mysql-server -y
```
<img width="975" height="331" alt="image" src="https://github.com/user-attachments/assets/820c9806-8d2d-4621-aac4-8f15b1f52491" />
 

- Install PHP and required modules. PHP works with Apache and MySQL to run dynamic applications. Run;
```bash
sudo apt install php libapache2-mod-php php-mysql -y
```
<img width="975" height="365" alt="image" src="https://github.com/user-attachments/assets/b381fa65-ad6e-495e-b569-e334bca00101" />
 
- Start and Enable Apache Service. We start Apache and enable it to run automatically at boot. Run;
```bash
sudo systemctl start apache2
sudo systemctl enable apache2
``` 
<img width="975" height="270" alt="image" src="https://github.com/user-attachments/assets/113ce65a-aace-41ed-b2c5-0cd21a37d9dc" />

- Start and MySQL Service. Run;
```bash
sudo systemctl start mysql
sudo systemctl enable mysql
```
<img width="975" height="273" alt="image" src="https://github.com/user-attachments/assets/8c2ea4d2-d49a-485b-a8d8-21feade16b48" />


- Verify Apache Service Status. Check if Apache is active and running. Run;
```bash
sudo systemctl status apache2
```
<img width="975" height="436" alt="image" src="https://github.com/user-attachments/assets/5ca0dc71-326a-4111-823e-b7ab08e42dfc" />
 
(Press q to quit the status screen.)

- Verify MySQL Service Status. Check if MySQL is active and running.
```bash
sudo systemctl status mysql
```
<img width="975" height="383" alt="image" src="https://github.com/user-attachments/assets/2a1ee9c9-7d97-49ef-843a-aa8499f0c73a" />
 
(Press q to quit.)

## Conclusion
Through this project, students gained practical, end-to-end experience in deploying and managing a server in the cloud. They learned how to launch an EC2 instance on AWS, configure SSH access with secure key pairs, and apply server hardening techniques to protect against common threats. By installing and verifying the LAMP stack — Linux, Apache, MySQL, and PHP — they prepared the instance to host dynamic web applications, just as real-world organizations require. This exercise not only reinforced their Linux administration skills but also built confidence in managing cloud infrastructure, applying security best practices, and delivering a functional server environment ready for application deployment. These competencies are foundational for modern DevOps roles and directly transferable to enterprise environments where reliability, security, and scalability are critical.








