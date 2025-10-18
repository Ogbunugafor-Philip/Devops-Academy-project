
# Building-a-3-Tier-VPC-Infrastructure-with-a-Public-and-Private-Subnet

![image](https://github.com/user-attachments/assets/4af3f410-a0d5-4cdd-9288-0d3e74ed54f5)

## Introduction
In today’s cloud-driven landscape, businesses demand highly secure, reliable, and scalable network environments to host their applications and manage sensitive data. This project focuses on leveraging Amazon Web Services (AWS) to design and implement a Virtual Private Cloud (VPC), providing an isolated and customizable network environment tailored to modern business needs.
The AWS VPC is a foundational service that allows organizations to deploy resources such as servers, databases, and applications in a secure, private network. By carefully designing and configuring the VPC, this project aims to demonstrate how enterprises can achieve optimal performance, enhanced security, and seamless integration with on-premises systems and other cloud resources.

## Statement of the Problem
As cloud infrastructures continue to grow in complexity, many organizations struggle with how to securely separate public-facing applications from sensitive backend systems such as databases. Without proper network segmentation, critical resources remain exposed, increasing the risk of cyberattacks, data breaches, and unauthorized access. Additionally, improperly configured VPC networking often leads to connectivity failures, operational inefficiencies, and limited scalability.
This project addresses these challenges by designing a structured 3-Tier VPC architecture that ensures secure isolation of resources, controlled internet access, and high availability across multiple availability zones, thereby providing a strong foundation for deploying modern cloud applications.

## Objectives
- To establish a secure and scalable networking environment.
- To enable internet connectivity for public resources.
- To segregate network traffic for enhanced security.
- To optimize resource configuration for accessibility and functionality.

## Project Steps

Step 1: Create a VPC

Step 2: Enable DNS Host Name

Step 3: Create Internet Gate Way

Step 4: Attach Internet Gateway to VPC

Step 5: Create Public Subnets

Step 6: Enable auto assign Public IPv4 address

Step 7: Create Route Tables

Step 8: Edit Association to allow Public Subnet access to the Internet

Step 9: Create the Private Subnets (Webserver and Database server)

## Project Implementation

### Step 1: Create a VPC
A Virtual Private Cloud (VPC) is a secure, isolated section of a public cloud where users can deploy resources with complete control over networking. It provides enhanced security, scalability, and control over how resources communicate internally and with the internet.
Our VPC would be created in the us-east-1 region. Resources would be created of two Availability Zones ( Availability Zone 1a and Availability Zone 1b) for high availability.

- Search for VPC in the search bar and click on it
  <img width="871" height="235" alt="image" src="https://github.com/user-attachments/assets/636e3019-1423-49c1-9baf-1f7fbdd15b9c" />

 

- Click on create VPC
 <img width="866" height="189" alt="image" src="https://github.com/user-attachments/assets/a7242c40-66a7-46da-9108-19495e9ffb04" />


- Fill the VPC creation request
  <img width="975" height="490" alt="image" src="https://github.com/user-attachments/assets/6ce2626d-c5d2-4540-8a03-8a125e5d2588" />

 

NOTE: The 10.0.0.0/16 CIDR block for my VPC defines the range of private IP addresses available for use within your Virtual Private Cloud (VPC). This implies that
  - The VPC can accommodate IP addresses from 10.0.0.0 to 10.0.255.255 (65,536 IP addresses)
  - Subnets can be created within this range by further dividing the CIDR block (e.g., 10.0.1.0/24, 10.0.2.0/24, etc.)
    
- Click on create VPC
  <img width="919" height="233" alt="image" src="https://github.com/user-attachments/assets/58e9032a-0b2c-4045-88b6-364df56586af" />

 
### Step 2: Enable DNS Host Name
There are two major reasons why we enable DNS Host Name.

Public DNS Names for EC2 Instances: When you turn on DNS hostnames in your VPC, any instance with a public IP gets a friendly name (like ec2-1-2-3-4.compute.amazonaws.com) instead of just an IP address (like 1.2.3.4).

This makes life easier because:

  - You can use the name instead of the IP to connect to your server (like when you use SSH).
  - If you’re hosting a website or app on the server, people can use this name to access it instead of remembering some random numbers.

Internal DNS Names for Private Resources: For servers inside your VPC (without public IPs), they also get friendly names to talk to each other within the network.

This is super handy because:
  
  - Servers can communicate using these names instead of keeping track of ever-changing IPs.
  - Imagine you have a database and a web server—they can easily find and talk to each other using these names, like calling each other by a nickname instead of a phone number.
    
To enable DNS Host Name,

- On your created VPC dashboard, click on Action and select edit VPC settings
 <img width="919" height="226" alt="image" src="https://github.com/user-attachments/assets/35ba45f4-0436-45bf-9b45-9fe15f2b617a" />

- Check the enable DNS hostnames and click on save
 <img width="863" height="183" alt="image" src="https://github.com/user-attachments/assets/6fb32c4f-4010-49f4-9ea5-a5c957e60cda" />

### Step 3: Create Internet Gate Way
An Internet Gateway is a bridge that allows a private network to connect to the internet, making it possible for devices in the network to access online services.

- Click on Internet Gateway
 <img width="781" height="124" alt="image" src="https://github.com/user-attachments/assets/7bc9537c-185b-4b2c-9ba0-23fec2ba74e6" />


- Click in create Internet Gateway
 <img width="801" height="90" alt="image" src="https://github.com/user-attachments/assets/67e4d071-55e8-46ed-961e-28b7f47773ba" />


- Select an internet gateway name and click create internet gateway
 <img width="811" height="239" alt="image" src="https://github.com/user-attachments/assets/f2d64831-57e7-4fbf-b95c-510933ccedb8" />
 

### Step 4: Attach Internet Gateway to VPC
- On the newly created Internet Gateway Page, click on action and select attach to VPC
 <img width="975" height="239" alt="image" src="https://github.com/user-attachments/assets/798bbd01-43c2-419b-91a7-4ddee6bf1304" />


- From the available VPCs, select the VPC we just created and click on Attach Internet gateway
 <img width="975" height="235" alt="image" src="https://github.com/user-attachments/assets/9b49fba5-8b92-412d-b6b3-5a2833838c97" />

### Step 5: Create Public Subnets
A public subnet is a subnet in a VPC that has a route to the internet through an internet gateway, allowing direct communication with external networks.
As highlighted in the beginning, our VPC resources  would be created of two Availability Zones ( Availability Zone 1a and Availability Zone 1b) for high availability.

Public Subnet AZ 1
- Click on subnet and select create subnet
 <img width="915" height="289" alt="image" src="https://github.com/user-attachments/assets/6af66b79-8470-4ca8-9f5a-17f7f013bfab" />


- Select VPC ID that the subnet would be created in
 <img width="899" height="280" alt="image" src="https://github.com/user-attachments/assets/d4eea5e4-9770-4af5-a706-34bc668a746d" />



- Enter the subnet settings and click create subnet
  - Subnet Name: Public_Subnet_AZ_1
  - Availability Zone: us-east-1a
  - Subnet CIDR: 10.0.0.0/24
 
<img width="975" height="329" alt="image" src="https://github.com/user-attachments/assets/21408994-da07-47e6-8ca7-ab839156ea1d" />


Public Subnet AZ 2
- Click on subnet and select create subnet
 <img width="915" height="289" alt="image" src="https://github.com/user-attachments/assets/f69c8439-08a7-4649-aa51-4832eede1ec4" />


- Select VPC ID that the subnet would be created in
 <img width="899" height="304" alt="image" src="https://github.com/user-attachments/assets/ca1dcbb9-2c26-4511-9bbd-48be4d34d888" />


- Enter the subnet settings and click create subnet
  - Subnet Name: Public_Subnet_AZ_2
  - Availability Zone: us-east-1b
  - Subnet CIDR: 10.0.1.0/24
    <img width="869" height="341" alt="image" src="https://github.com/user-attachments/assets/af15bf13-5465-4e03-a72a-ca0c5f3db8f0" />

 
### Step 6: Enable auto assign Public IPv4 address
Enabling auto-assign IPv4 addresses allows instances to automatically receive public IPs for internet access.
- Check the public subnet box, select actions and click edit subnet settings
<img width="975" height="258" alt="image" src="https://github.com/user-attachments/assets/9854059c-aa9f-4617-b68e-1dd26ce4268a" />
 

- Check the box of enable auto assign public IPv4 address and click save.
 <img width="975" height="181" alt="image" src="https://github.com/user-attachments/assets/1e78d3cf-e192-45c9-bf1c-d88fc601648b" />
 

Do same for the other Public Subnet created


### Step 7: Create Route Tables
A route table is like a map that tells data where to go across a network, defining how traffic is directed between subnets, networks, or devices based on destination IP addresses.
- Go to route table  then click on create route table
<img width="975" height="222" alt="image" src="https://github.com/user-attachments/assets/d2e10d89-4719-4faf-8cb3-3609a1acd25f" />
 

- Give the route table a name, select the VPC we created and then click create route table
 <img width="975" height="285" alt="image" src="https://github.com/user-attachments/assets/7c592b2e-26a6-4fea-bb25-9bca55819c26" />


Note: The created route table cannot access the internet.
For the route table to be able to access the internet,

- Click on edit route
 <img width="920" height="169" alt="image" src="https://github.com/user-attachments/assets/2e331cd6-ac42-482f-bf70-9d2bf5508a5b" />

- Add route from anywhere (0.0.0.0/0), then select Internet gateway (the one we just created), then click save changes
 <img width="975" height="210" alt="image" src="https://github.com/user-attachments/assets/df8c6236-4714-43b7-a4bc-141677a6e4f9" />

### Step 8: Edit Association to allow Public Subnet access to the Internet
By default, our Public subnet cannot access the internet, so any resources created on them cannot access the internet. To all internet access on our public subnet,
- Go to subnet association then click on edit subnet association
 <img width="975" height="189" alt="image" src="https://github.com/user-attachments/assets/a44e4ce3-fdf4-4963-9c29-6f00bdac8974" />


- Select our two created Public Subnet and click on save association
 <img width="975" height="254" alt="image" src="https://github.com/user-attachments/assets/03aa9744-adad-4afb-aef1-b87824a2c775" />

### Step 9: Create the Private Subnets (Webserver and Database server)
A private subnet is a segment of a network that is isolated from the internet, allowing resources within it to communicate internally while restricting direct external access for security purposes.
As highlighted in the beginning, our VPC resources  would be created of two Availability Zones ( Availability Zone 1a and Availability Zone 1b) for high availability.

Private Subnet AZ 1 (Webserver and Database)

- Click on subnet and select create subnet
 <img width="778" height="298" alt="image" src="https://github.com/user-attachments/assets/863f8bc8-3538-486f-aac2-8b829b4be7f1" />



- Select VPC ID that the subnet would be created in
 <img width="899" height="280" alt="image" src="https://github.com/user-attachments/assets/f209d4e5-769f-48c0-acef-900096fe2175" />


- Enter the subnet settings and click create subnet
  - Subnet Name: Webserver_Subnet_AZ_1
  - Availability Zone: us-east-1a
  - Subnet CIDR: 10.0.2.0/24
    <img width="746" height="329" alt="image" src="https://github.com/user-attachments/assets/b308cb50-7ca4-455b-b40e-c3516df338dc" />

 
Database Server AZ 1 Creation

- Click on subnet and select create subnet
 <img width="778" height="298" alt="image" src="https://github.com/user-attachments/assets/0e5d6d0f-654f-4985-a838-a7f49ec2b6b6" />


- Select VPC ID that the subnet would be created in
 <img width="899" height="280" alt="image" src="https://github.com/user-attachments/assets/70884e96-7649-44c7-899e-d8fcac474fd0" />


- Enter the subnet settings and click create subnet
  - Subnet Name: Database_Subnet_AZ_1
  - Availability Zone: us-east-1a
  - Subnet CIDR: 10.0.4.0/24
 
<img width="790" height="306" alt="image" src="https://github.com/user-attachments/assets/4dd1cf37-f7b6-477c-8274-1418ab44daa4" />


Private Subnet AZ 2 (Webserver and Database)

- Click on subnet and select create subnet
 <img width="778" height="298" alt="image" src="https://github.com/user-attachments/assets/0b523c8c-abfe-4cd3-bd42-3968b8caf61c" />



- Select VPC ID that the subnet would be created in
  <img width="899" height="280" alt="image" src="https://github.com/user-attachments/assets/057306e9-63ca-41b7-9d8a-23c410d618e4" />

 

- Enter the subnet settings and click create subnet
  - Subnet Name: Webserver_Subnet_AZ_2
  - Availability Zone: us-east-1b
  - Subnet CIDR: 10.0.3.0/24
 <img width="853" height="395" alt="image" src="https://github.com/user-attachments/assets/ab227dc9-e294-4ddd-aa34-b795bbb53521" />


Database Server AZ 2 Creation

- Click on subnet and select create subnet
 
<img width="778" height="298" alt="image" src="https://github.com/user-attachments/assets/dc247e9c-049e-447c-9832-1fbbfef57fff" />


- Select VPC ID that the subnet would be created in
 <img width="899" height="248" alt="image" src="https://github.com/user-attachments/assets/0e7e4f45-9b0a-4df3-8c02-75f5482e88a3" />


- Enter the subnet settings and click create subnet
  - Subnet Name: Database_Subnet_AZ_2
  - Availability Zone: us-east-1b
  - Subnet CIDR: 10.0.5.0/24
 <img width="873" height="326" alt="image" src="https://github.com/user-attachments/assets/f2b001be-0737-45de-9558-20fb090b812f" />

Any subnets that have not been explicitly associated with any route tables are associated with the main route table

### Conclusion
In conclusion, the outlined steps provide a structured approach to setting up a secure and functional networking environment in the cloud. By creating a Virtual Private Cloud (VPC), enabling DNS hostnames, and configuring public and private subnets, the project ensures both accessibility for public-facing resources and isolation for critical backend components. The integration of an Internet Gateway, route tables, and automated IP assignment enhances connectivity and resource management. This setup establishes a robust foundation for hosting scalable and secure applications, meeting both operational and security requirements.

