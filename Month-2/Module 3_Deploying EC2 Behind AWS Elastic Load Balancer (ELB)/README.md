# Module 3_Deploying EC2 Behind AWS Elastic Load Balancer (ELB)

## Introduction
In cloud-based architectures, reliability and scalability are achieved through load balancing, a mechanism that intelligently distributes incoming network traffic across multiple servers. Without it, applications risk downtime or degraded performance under heavy load.
Amazon Web Services (AWS) provides the Elastic Load Balancer (ELB) service, which automatically spreads application traffic across multiple targets (EC2 instances, containers, or IPs) within one or more Availability Zones.
This project introduces the core concepts of load balancing and provides practical experience in configuring an AWS ELB to handle and distribute traffic across multiple EC2 instances efficiently.

## Statement of the Problem
Many traditional web applications rely on a single server setup, which quickly becomes a performance bottleneck as user traffic increases. When that server fails, the entire application becomes unavailable, leading to service interruptions and user dissatisfaction.
To ensure high availability and fault tolerance, organizations must implement mechanisms that distribute incoming traffic evenly and automatically reroute users when a server fails; a challenge effectively addressed through load balancing.

## Project Objectives
a. Understand the concepts and importance of load balancing in cloud environments.

b.Learn the basics of AWS Elastic Load Balancer (ELB) configuration.
c. Deploy multiple EC2 instances and connect them behind a Load Balancer.

d. Test real-time traffic distribution and fault tolerance.

e. Demonstrate how load balancing improves scalability and uptime.

## Project Steps

Step 1: Launch two EC2 instances running the same web application 

Step 2: Create a Target Group in AWS to register both EC2 instances.

Step 3: Configure an Application Load Balancer (ALB) and attach the target group.


## Project Implementation
### Step 1: Launch two EC2 instances running the same web application 

In this step, you will create two virtual servers (EC2 instances) that host the same web application. This setup allows traffic to be shared between both servers instead of relying on one.
By running the same website on two EC2 instances, you prepare the environment for load balancing. If one server goes down, the other continues to serve users without interruption. This step helps you understand how AWS ensures better uptime and performance through redundancy.

- Create a key pair (for SSH login to both servers)
  - Go to EC2 → Network & Security → Key pairs → Create key pair
    <img width="914" height="352" alt="image" src="https://github.com/user-attachments/assets/04ae9f90-fbdf-4dff-898d-0ba1461b6969" />

 
  - Name: devops-academy-key
  - Type: RSA | File format: .pem
  - Click Create key pair and save the .pem file safely on your computer.
    <img width="911" height="473" alt="image" src="https://github.com/user-attachments/assets/ff89c2cd-d512-498e-816c-8a8bdb442811" />

 

- Launch the First EC2 Instance (Server 1). Go to your AWS Management Console → EC2 → Instances → Launch instances

  Configure as follows:
    - Name: web-server-1
    - AMI: Ubuntu Server 22.04 LTS
      <img width="914" height="366" alt="image" src="https://github.com/user-attachments/assets/5e613eb8-8eb1-4b06-a1d1-875e1b679211" />

   - Instance type: t3.micro (free tier)
   - Key pair: devops-academy-key
   - Network settings:
       - Allow HTTP (port 80)
       - Allow SSH (port 22)
         <img width="861" height="269" alt="image" src="https://github.com/user-attachments/assets/b038b454-8693-4f84-a11f-99aad6072f09" />

 
  - Storage: Default (8 GB is fine)
  - Click Launch Instance.
    <img width="975" height="186" alt="image" src="https://github.com/user-attachments/assets/a5090add-5bed-4d1e-b8f6-670a6b224f3a" />

 





- Open your gitbash and navigate to where you have your .pem saved
```
cd Downloads
```
- Run the command to ssh into your created server;
```
chmod 400 devops-academy-key.pem
```
<img width="884" height="255" alt="image" src="https://github.com/user-attachments/assets/a44ec466-3210-4312-b4ee-587cebfdd1d7" />


```
ssh -i "devops-academy-key.pem" ubuntu@<Public-IP-of-Server-1>
```
<img width="975" height="160" alt="image" src="https://github.com/user-attachments/assets/d19cfc08-a5c3-4ba8-8f57-292caa31ddb6" />


- Install and Configure a Simple Web Server. Run these commands on Server 1 one after another
```
sudo apt update -y
sudo apt install apache2 -y
sudo systemctl enable apache2
sudo systemctl start apache2
sudo systemctl status apache2
 ```
<img width="975" height="384" alt="image" src="https://github.com/user-attachments/assets/bfa8783b-e36d-41f3-a16e-36ca786eba46" />





- Then edit the homepage to identify this server. Run;
```
echo "<h1>Welcome to Server 1 - DevOps Academy</h1>" | sudo tee /var/www/html/index.html
``` 

- Test it by opening your server’s public IP in your browse
```
http://<webserver 1 public ip>
```
 <img width="905" height="166" alt="image" src="https://github.com/user-attachments/assets/919e0bca-699d-4f57-91a2-6ed4591e0354" />


Now let us do the same for server 2

- Launch the First EC2 Instance (Server 1). Go to your AWS Management Console → EC2 → Instances → Launch instances

  Configure as follows:
    - Name: web-server-2
    - AMI: Ubuntu Server 22.04 LTS
      <img width="914" height="366" alt="image" src="https://github.com/user-attachments/assets/5e613eb8-8eb1-4b06-a1d1-875e1b679211" />

   - Instance type: t3.micro (free tier)
   - Key pair: devops-academy-key
   - Network settings:
       - Allow HTTP (port 80)
       - Allow SSH (port 22)
         <img width="861" height="269" alt="image" src="https://github.com/user-attachments/assets/b038b454-8693-4f84-a11f-99aad6072f09" />

 
  - Storage: Default (8 GB is fine)
  - Click Launch Instance.
    <img width="975" height="186" alt="image" src="https://github.com/user-attachments/assets/a5090add-5bed-4d1e-b8f6-670a6b224f3a" />

 


- Open your gitbash and navigate to where you have your .pem saved
```
cd Downloads
```
- Run the command to ssh into your created server;
```
chmod 400 devops-academy-key.pem
```
<img width="884" height="255" alt="image" src="https://github.com/user-attachments/assets/a44ec466-3210-4312-b4ee-587cebfdd1d7" />


```
ssh -i "devops-academy-key.pem" ubuntu@<Public-IP-of-Server-1>
```
<img width="975" height="160" alt="image" src="https://github.com/user-attachments/assets/d19cfc08-a5c3-4ba8-8f57-292caa31ddb6" />


- Install and Configure a Simple Web Server. Run these commands on Server 1 one after another
```
sudo apt update -y
sudo apt install apache2 -y
sudo systemctl enable apache2
sudo systemctl start apache2
sudo systemctl status apache2
 ```
<img width="975" height="384" alt="image" src="https://github.com/user-attachments/assets/bfa8783b-e36d-41f3-a16e-36ca786eba46" />




- Then edit the homepage to identify this server. Run;
```
echo "<h1>Welcome to Server 2 - DevOps Academy</h1>" | sudo tee /var/www/html/index.html
``` 

- Test it by opening your server’s public IP in your browse
```
http://<webserver 2 public ip>
```
<img width="975" height="144" alt="image" src="https://github.com/user-attachments/assets/763efd38-ba6a-41b8-a037-41b071e9f5cb" />


## Step 2: Create a Target Group in AWS to register both EC2 instances
In AWS, a Target Group acts as the logical collection of servers (EC2 instances, containers, or IP addresses) that a Load Balancer distributes traffic to. When users access an application through the Load Balancer, the requests are forwarded to one of the healthy targets in this group.
By creating a target group, you define where and how your load balancer will send incoming traffic. It also enables health checks, which automatically monitor each registered instance to ensure it is responsive. If one instance becomes unhealthy, traffic is rerouted to the remaining healthy instances — ensuring high availability and fault tolerance for your application.

- In the AWS Console, go to EC2 → Target Groups (under Load Balancing). Click Create target group
  <img width="975" height="392" alt="image" src="https://github.com/user-attachments/assets/71482e00-5f1e-43d8-a20a-c7d39c248d9c" />

 
- Configure Target Group settings. Fill in the form as follows:
    - Target type: Instances
      <img width="922" height="300" alt="image" src="https://github.com/user-attachments/assets/51cccf1a-9110-4719-992d-ddf3f16b923d" />

   - Target group name: devops-academy-tg
   - Protocol: HTTP
   - Port: 80
     <img width="923" height="386" alt="image" src="https://github.com/user-attachments/assets/b7cfdbad-647a-4daa-9d49-9da3e4f336f3" />

     
   - VPC: Choose the same VPC where your EC2 servers are running (default)
   - Health checks: HTTP
   - Health check path: / (leave as default)
   - Click next
     <img width="889" height="186" alt="image" src="https://github.com/user-attachments/assets/d8b41a35-745c-4f40-9503-088013cfbe54" />

	
- Register Targets (Your Servers). You’ll see both your EC2 instances listed.
  Check the boxes beside:
    - web-server-1
    - web-server-2
      <img width="906" height="269" alt="image" src="https://github.com/user-attachments/assets/1eb4cf0c-dedc-405d-a024-28a5e2a8e9c9" />

 
- Click Include as pending below.
  <img width="931" height="275" alt="image" src="https://github.com/user-attachments/assets/2eaf2dbb-5eae-40f4-a646-b27ba0ab412b" />

- Scroll down and click Create target group.
  <img width="975" height="348" alt="image" src="https://github.com/user-attachments/assets/4c7f99fe-83b4-42e8-afdf-89ec4688d51e" />

 


### Step 3: Configure an Application Load Balancer (ALB) and attach the target group

An Application Load Balancer (ALB) intelligently distributes incoming web traffic across multiple targets such as EC2 instances to ensure no single server becomes overloaded. 
In this step, we would create an Application Load Balancer in AWS and link it to the target group you created earlier. Once configured, the ALB will begin performing health checks on each registered EC2 instance and automatically route traffic to healthy servers only. This ensures high availability, scalability, and fault tolerance for your web application.
After successful setup, when users access the Load Balancer’s DNS name, AWS will distribute their requests alternately between WebServer 1 and WebServer 2, proving that load balancing is active.

- In your AWS Management Console, go to: EC2 → Load Balancers (under Load Balancing). Click Create Load Balancer.
  <img width="975" height="278" alt="image" src="https://github.com/user-attachments/assets/a54e9508-7bc7-44a1-8391-4776a6400dce" />

 - Under the Application Load Balancer section, click Create.
   <img width="975" height="511" alt="image" src="https://github.com/user-attachments/assets/c6087c95-b0ae-4cb0-9997-bd2fd72f91f3" />

 
- Fill in the following details:
    - Name: devops-academy-alb
    - Scheme: Internet-facing
    - IP address type: IPv4
      <img width="941" height="404" alt="image" src="https://github.com/user-attachments/assets/895283ef-43b7-4e24-9a27-986633ec18fd" />

      
 
- Select the same VPC where your EC2 instances are running.
  Availability Zones:
    - Choose two Availability Zones (example: us-east-1a and us-east-1b).
    - For each zone, select the public subnet associated with it.
      <img width="935" height="560" alt="image" src="https://github.com/user-attachments/assets/41ab2e05-c3d7-4d05-a3a3-9c635f5cd350" />

 
This ensures redundancy — if one zone fails, the other keeps serving traffic.

- To configure Security Groups
    - Choose Select an existing security group.
    - Pick the same one used by your EC2 instances (or create a new one).
    - Ensure Inbound Rules allow HTTP (port 80) access from anywhere (0.0.0.0/0).
 

- Configure Listeners and Routing
- Under Listeners, you’ll see:
    - Protocol: HTTP
    - Port: 80
- Under Default action, choose:
    - Forward to → select your existing target group devops-academy-tg.
      <img width="953" height="393" alt="image" src="https://github.com/user-attachments/assets/66cddc25-4247-4f3b-b352-ece936c022ce" />

 


- Review all configurations. Click Create Load Balancer. Wait a few minutes until the Status changes to Active.
  <img width="975" height="155" alt="image" src="https://github.com/user-attachments/assets/bc73a9ac-9abc-4d43-af70-031b258b7b19" />

 

- Once the ALB moves from provisioning to active after a few minutes of creation;
  <img width="975" height="302" alt="image" src="https://github.com/user-attachments/assets/1c09132f-963f-4496-97eb-e0f449a7423f" />

 

  - Go to EC2 → Target Groups → devops-academy-tg → Targets tab.
  - You should now see your two EC2 instances listed as Healthy after AWS runs its health checks.
    <img width="926" height="217" alt="image" src="https://github.com/user-attachments/assets/0932ef39-8e4f-4e10-9b3f-f5350aec6ebc" /> 

If both are marked Healthy, it means your ALB is successfully routing traffic.


- To test the Load Balancer
    - Go to your Load Balancer → Description tab.
    - Copy the DNS name (something like devops-academy-alb-123456.us-east-1.elb.amazonaws.com).
      <img width="922" height="384" alt="image" src="https://github.com/user-attachments/assets/b5634960-f0d2-4e9d-9846-971ace88b794" />

 
- Paste that URL into your browser and refresh several times.
  You should see alternating responses:

- “Welcome to Server 1 - DevOps Academy”
  <img width="926" height="164" alt="image" src="https://github.com/user-attachments/assets/28a7ccea-e91a-4927-9c0e-18d418da610b" />


- “Welcome to Server 2 - DevOps Academy”
  <img width="933" height="159" alt="image" src="https://github.com/user-attachments/assets/f896b3d7-f404-4c7f-b185-03c44c3a3bb4" />

 
That confirms your Application Load Balancer is working perfectly 

## Conclusion
This project successfully demonstrated how to deploy multiple EC2 instances behind an AWS Elastic Load Balancer (ELB) to achieve high availability, scalability, and fault tolerance in a cloud environment. Through the practical implementation, two identical web servers were launched and configured to serve the same web application. A target group was then created to register both instances, and an Application Load Balancer (ALB) was configured to intelligently distribute incoming traffic between them.
By accessing the Load Balancer’s DNS name, alternating responses from Server 1 and Server 2 confirmed that the load balancer was functioning as expected. This ensured that user requests were automatically routed to healthy instances, maintaining continuous service even if one server became unavailable.
In essence, this project provided hands-on experience with one of AWS’s core services for building resilient, production-grade architectures. It highlights how ELB contributes to system reliability, minimizes downtime, and supports seamless horizontal scaling — essential principles for any modern cloud infrastructure.















