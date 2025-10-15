# Module 2_SecureWeb – Configuring Apache for HTTPS with Self-Signed SSL

## Introduction

In modern web infrastructure, the need for secure communication between clients and servers is non-negotiable. HTTP, which stands for HyperText Transfer Protocol, governs how data is transferred over the web. However, because HTTP transmits information in plain text, it is vulnerable to interception and tampering by attackers. To solve this, SSL/TLS (Secure Sockets Layer / Transport Layer Security) protocols were introduced to encrypt communication, ensuring confidentiality, integrity, and authenticity of transmitted data.
This project focuses on understanding the fundamentals of HTTP and HTTPS, exploring how SSL/TLS secures network transactions, and configuring an Apache web server to use a self-signed SSL certificate for HTTPS connections. By completing it, learners gain practical insight into how encryption is implemented in real-world web systems and how secure web services are deployed.

## Statement of the Problem
Many web applications still operate over insecure HTTP connections, exposing sensitive information such as login credentials and session cookies to potential interception. Small organizations or beginners often avoid HTTPS because of perceived complexity or cost associated with obtaining certificates from trusted Certificate Authorities (CAs).
This lack of encryption increases the risk of data breaches, man-in-the-middle (MITM) attacks, and loss of user trust. Therefore, there is a need to demonstrate a low-cost, practical approach to securing web servers using self-signed certificates — enabling secure HTTPS connections even in non-production or internal environments.

## Project Objective

i.	Understand how HTTP request/response mechanisms work.

ii.	Explain the principles of SSL/TLS and HTTPS communication.

iii.	Configure and test an Apache web server with a self-signed SSL certificate.

iv.	Validate secure connectivity using HTTPS and browser inspection tools.

v.	Establish foundational knowledge for future integration with Let’s Encrypt or Cloud-based certificates in production environments.

## Project Steps

Step 1 – Set Up the Project Environment

Step 2 – Generate a Self-Signed SSL Certificate

Step 3 – Configure Apache for HTTPS

Step 4 – Enable SSL and Apply Configuration

Step 5 – Test and Verify HTTPS Connection

## Project Implementation
### Step 1 – Set Up the Project Environment
Before implementing HTTPS or configuring SSL certificates, it is essential to establish a stable and functional web server environment. Step 1 focuses on preparing the foundational setup required for the entire project.
In this stage, you will deploy an Ubuntu 20.04 server, perform all necessary system updates, and install the Apache web server, which will serve as the platform for enabling HTTPS later. Ensuring Apache runs correctly and is accessible over HTTP provides the baseline confirmation that the server environment is properly configured.
This preparation step ensures that the system is secure, up-to-date, and ready to host SSL/TLS configurations in subsequent stages.

- Visit the AWS Website
    - Go to the official AWS homepage: https://aws.amazon.com
    - Click “Create an AWS Account” at the top right corner of the page.
      <img width="951" height="813" alt="image" src="https://github.com/user-attachments/assets/f2b2f754-5ac0-43f5-8a48-c447429a7f4b" />

 
- Select New to AWS? Sign up
 <img width="547" height="589" alt="image" src="https://github.com/user-attachments/assets/45874618-d4a1-44b2-b798-45c47e2c459b" />


- Enter Account Details
    - Provide a valid email address that will be tied to your AWS root account.
    - Create a strong password for security.
    - Enter an AWS account name (this will identify your account).
- Verify Email Address
    - AWS sends a verification code or link to the email you provided.
    - Open your email inbox and verify the account to continue registration.
- Choose Account Type
    - Select Personal (for individual use) or Professional (for business/organization).
    - Fill in your name, phone number, and country/region.
    - Provide a valid billing address for verification.
- Add Payment Method
    - Enter a credit/debit card or an internationally accepted virtual card (e.g., Visa, Mastercard).
    - AWS will charge a small temporary fee (usually $1) for card verification, which is refunded.
    - Confirm that your card is active and authorized for online transactions.
- Verify Identity
  - Choose a phone verification method (SMS or voice call).
  - Enter the code sent to your phone to confirm your identity.
  - Select a Support Plan
  - Basic (Free) – Suitable for beginners.
- Sign In to the AWS Management Console
  - After successful verification, go to
    ```
    https://console.aws.amazon.com.
    ```
  - Log in with your root email and password.
  - You now have full access to AWS services.
- Log on to the just created AWS. In the search bar, type EC2 and open the service
 <img width="975" height="263" alt="image" src="https://github.com/user-attachments/assets/38cec9c3-dc7b-46b2-ab5d-7ded6f08ee38" />


- Click Instance then, launch Instance to begin the setup. Fill the below;
 <img width="975" height="329" alt="image" src="https://github.com/user-attachments/assets/153a697a-61ee-41fe-be90-d6c6752ea880" />


  - Name: SecureWeb-Server
  - AMI (Amazon Machine Image): Choose Ubuntu Server 22.04 LTS
  - Instance Type: t3.micro (free tier eligible)
    <img width="908" height="390" alt="image" src="https://github.com/user-attachments/assets/8353bebd-bc20-4ebf-8ff5-863aac164c4e" />

 
- Key Pair: Create a new one (e.g., secureweb-key)
  <img width="917" height="425" alt="image" src="https://github.com/user-attachments/assets/4a1bb6e1-3be2-4b52-aff3-ffcd7f566fb6" />
 
 

- Scroll down and click launch instance
 <img width="975" height="164" alt="image" src="https://github.com/user-attachments/assets/7ee03e91-3d81-44a9-b56f-21e968eb772a" />


- Now that our instance is running, let us configure the security group. Click security and then security group
 <img width="975" height="198" alt="image" src="https://github.com/user-attachments/assets/68288c42-a81c-49f9-b4cb-c4b9c1af5400" />


- Click on edit inbound rule
 <img width="975" height="185" alt="image" src="https://github.com/user-attachments/assets/9ed22e06-11d0-4110-be87-cc4d4a6098a5" />




- Fill the below with the screenshot guide and save
 <img width="975" height="311" alt="image" src="https://github.com/user-attachments/assets/bb2ba470-e1cd-4ed1-acd9-e51a52520878" />


#### Understanding the security configuration:
  - SSH (22) → Restricted to your IP for ssh→ ✅ Secure
  - HTTP (80) → Open for web traffic → ✅ Required
  - HTTPS (443) → Open for secure traffic → ✅ Required

- Next, lets us SSH into our just created AWS server. Open your git bash and go to where you have your .pem saved (downloads). Run the command;
```
cd Downloads
``` 
<img width="975" height="257" alt="image" src="https://github.com/user-attachments/assets/d1558581-8046-45c1-9a4e-47fcb70c1baa" />

- Run this command to ssh into our AWS Server from our git bash
```
ssh -i secureweb-key.pem ubuntu@<Public-IP-Address>
```
Replace public IP Address with your server public ip address
 <img width="975" height="273" alt="image" src="https://github.com/user-attachments/assets/dbd49f7e-62ef-4a7f-8dc5-9bb318990868" />


- Now that we are connected to our instance from our local host, let us update the package list. Run;
```
sudo apt update
```
<img width="975" height="365" alt="image" src="https://github.com/user-attachments/assets/61956ff6-5b53-44a0-8b14-3d33456c2258" />


- Now let us upgrade the packages. Run;
```
sudo apt upgrade -y
``` 
<img width="975" height="306" alt="image" src="https://github.com/user-attachments/assets/8be96f1a-d38c-47da-835b-a176290d68a5" />

- Let us install and run the Apache web server, which will later be configured for HTTPS. This step ensures our server can serve web pages over HTTP before we add SSL. Run;
```
sudo apt install apache2 -y
``` 
<img width="975" height="300" alt="image" src="https://github.com/user-attachments/assets/e71f0b4c-08d4-4e77-aabd-3625dbe4f85e" />


- Run the following commands one after another to start, enable and see the status of Apache
```
sudo systemctl start apache2
sudo systemctl enable apache2
sudo systemctl status apache2
``` 
<img width="975" height="370" alt="image" src="https://github.com/user-attachments/assets/aeaf6a92-63d0-4eba-8694-75f29a4457ed" />

- Now lets confirm our Apache is configured correctly. Put you public IP in your browser in this format and see the outcome.
http://<Public-IP-Address>
<img width="975" height="677" alt="image" src="https://github.com/user-attachments/assets/39c6b30b-8940-4e94-92ca-2160a0bf795d" />
 

### Step 2 – Generate a Self-Signed SSL (Secure Sockets Layer) Certificate
In this step, we’ll create our own SSL certificate to enable secure HTTPS communication between clients and the Apache web server, without relying on a paid domain or external certificate authority.
Self-signed certificates are perfect for learning environments and internal testing because they provide the same encryption as commercial certificates, only lacking the third-party trust validation.
We’ll use OpenSSL, a powerful open-source tool, to generate two key files:
- A private key (kept secret on the server), and
- A public certificate (shared with clients).

Once completed, the server will be capable of serving HTTPS requests securely, using encryption to protect data in transit.

- Install OpenSSL if not already installed, run;
```
sudo apt install openssl -y
``` 
<img width="975" height="150" alt="image" src="https://github.com/user-attachments/assets/357dfee5-97a9-46b7-bbcb-0261e43f8bf8" />

- Verify that OpenSSL is installed by running,
```
openssl version
```
<img width="975" height="78" alt="image" src="https://github.com/user-attachments/assets/4b2fa210-52d8-4209-8da7-367ffc5d69cf" />


Let us create a secure private key and a self-signed SSL certificate that encrypts data on your Apache web server.
- Run this single OpenSSL command,
```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout /etc/ssl/private/apache-selfsigned.key \
-out /etc/ssl/certs/apache-selfsigned.crt
```
 <img width="975" height="344" alt="image" src="https://github.com/user-attachments/assets/89215b2c-e4ef-4150-9716-cc26cd6cab49" />


- When prompted for details, fill them as follows (below sample) (press Enter to skip optional fields)
    - Country Name: NG
    - State or Province Name: Kogi
    - Locality Name: Lokoja
    - Organization Name: DevOps Academy
    - Organizational Unit Name: Training
    - Common Name: Use your EC2 Public IP (e.g., 54.180.21.123)
    - Email Address: (press Enter to skip)
      <img width="975" height="180" alt="image" src="https://github.com/user-attachments/assets/4a92a34e-89b9-44d7-90e7-87fdf5af6f22" />

 

- Once complete, verify both files exist by running;
```
sudo ls -l /etc/ssl/certs/apache-selfsigned.crt /etc/ssl/private/apache-selfsigned.key
``` 
<img width="975" height="105" alt="image" src="https://github.com/user-attachments/assets/704c5c30-67ed-454b-9cc9-b7f43c760ffc" />

### Step 3 – Configure Apache for HTTPS
Now that the self-signed SSL certificate has been successfully generated, the next step is to configure Apache to use it for secure communication.
By default, Apache serves web pages over HTTP (port 80), which is not encrypted. To enable HTTPS (port 443), we must instruct Apache to:

- Use the SSL/TLS module,
- Load the certificate and private key we created, and
- Serve encrypted content to clients.

This configuration ensures that all data transferred between the server and users is encrypted, tamper-proof, and authenticated, preventing attacks like eavesdropping or data interception.
We’ll achieve this by creating a new Virtual Host configuration specifically for HTTPS, defining parameters like:

- Server name (EC2 IP or hostname)
- Document root (where the web files are stored)
- Paths to the SSL certificate and key

Once configured, Apache will be able to serve web pages securely over HTTPS, preparing the system for real-world encryption scenarios.

- Create a new configuration file for SSL using the vi text editor. Run;
```
sudo vi /etc/apache2/sites-available/secureweb-ssl.conf
```

- Paste the following configuration block inside the file. Make sure to replace your server’s name with your ec2 public IP. 
```
<VirtualHost *:443>
    ServerAdmin admin@secureweb.local
    ServerName  13.60.240.147
    DocumentRoot /var/www/html

    SSLEngine on
    SSLCertificateFile /etc/ssl/certs/apache-selfsigned.crt
    SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key

    <Directory /var/www/html>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
 ```
<img width="975" height="367" alt="image" src="https://github.com/user-attachments/assets/88d82327-b01b-465d-86c1-dd45a2d8f27b" />


- Confirm the file exists. Run;
```
sudo ls /etc/apache2/sites-available/secureweb-ssl.conf
``` 

### Step 4 – Enable SSL and Apply Configuration
After configuring Apache to use the self-signed SSL certificate, the next step is to activate SSL support and apply the new HTTPS configuration.
By default, Apache does not load the SSL module or enable secure sites automatically. In this step, we explicitly enable the SSL module and the newly created virtual host configuration so the web server can handle encrypted HTTPS traffic.
This process ensures that Apache recognizes the self-signed certificate, loads it into memory, and begins listening securely on port 443. Finally, the configuration changes are validated by restarting Apache and confirming that the service is active, error-free, and ready to accept secure connections.

- Enable the SSL module in Apache. Run;
```
sudo a2enmod ssl
``` 
<img width="975" height="264" alt="image" src="https://github.com/user-attachments/assets/aa0f3b01-af3d-40b2-975f-42f750c6b0fa" />

- Enable the new SSL site configuration. Run;
```
sudo a2ensite secureweb-ssl.conf
```
- Disable the default HTTP-only site. Run;
```
sudo a2dissite 000-default.conf
```
- Restart Apache to apply changes. Run;
```
sudo systemctl restart apache2
```
- Check Apache status. Run;
```
sudo systemctl status apache2
``` 
<img width="975" height="248" alt="image" src="https://github.com/user-attachments/assets/760ce91a-1c61-4b7d-a1db-745adc0555d4" />

- To confirm Port 443 is Listening for Secure Connections’ run;
```
sudo ss -tuln | grep 443
``` 
<img width="975" height="81" alt="image" src="https://github.com/user-attachments/assets/32e69051-e347-42fc-b5a8-df4a27410fca" />

### Step 5 – Test and Verify HTTPS Connection
With Apache now configured and SSL enabled, the final step is to test the secure connection to ensure HTTPS is functioning properly.
This verification step confirms that the self-signed certificate has been correctly installed and that encrypted communication between the server and clients is working as intended.
During this test, the browser will display a “connection not private” or “untrusted certificate” warning — this is normal for self-signed certificates since they are not issued by a trusted Certificate Authority (CA). The encryption, however, remains fully effective.
We will also verify the SSL certificate details (issuer, validity period, and encryption strength) using both a web browser and command-line tools.
Completing this step confirms that your Apache web server is capable of serving secure HTTPS traffic and that your SSL configuration is functioning correctly.

- Open your browser (Chrome, Firefox, Edge, or Safari). In the address bar, type your EC2 Public IP using the HTTPS protocol like this;
```
https://<your-public-ip>
```
<img width="975" height="305" alt="image" src="https://github.com/user-attachments/assets/7d542623-aca0-41be-9431-e978dc611d26" />
 
Everything worked perfectly but you’ll notice it saying not secure and the https is strike. This is the reason;
Browsers (like Chrome, Edge, or Firefox) only trust certificates issued by recognized Certificate Authorities (CAs) such as Let's Encrypt, DigiCert, or Comodo.
Because your certificate was self-signed, it wasn’t issued by any CA — it’s trusted by your server only, not by browsers.
So:
  - 🔐 Encryption is active — your traffic is still securely encrypted with SSL/TLS.
  - 🚫 Trust verification is missing — the browser just can’t confirm who the server really is, since there’s no third-party signature.

That’s why the browser marks it “Not Secure,” even though the connection is actually encrypted.

- Let us verify SSL Certificate Details Using Command Line. Run;
```
echo | openssl s_client -connect localhost:443 -servername localhost 2>/dev/null | openssl x509 -noout -text
```
 <img width="975" height="369" alt="image" src="https://github.com/user-attachments/assets/29826163-f35a-400f-ab21-e760578cabff" />

#### This command does two things:
  - Connects to your local server over port 443 (HTTPS).
  - Extracts and displays the certificate details currently in use.


#### Look for the following fields in the output:

  - Issuer: should say something like Issuer: CN = <your IP or secureweb.local>
  
  - Validity: should show your certificate’s start and end date (365 days).
    
  - Subject: should match the name or IP you entered as Common Name (CN).
    
  - Public Key / Signature Algorithm: confirms encryption strength (e.g., RSA 2048-bit).

## Conclusion
This project successfully demonstrated how to configure a secure web server environment using Apache and a self-signed SSL certificate on Ubuntu 22.04 (AWS EC2).
Through the step-by-step implementation, we explored the transition from HTTP to HTTPS, gaining practical experience in enabling encryption, protecting data integrity, and ensuring confidentiality in web communication. By generating and deploying a self-signed certificate, we proved that it is possible to achieve secure HTTPS connections without purchasing a domain or relying on a third-party Certificate Authority (CA) — making this approach ideal for internal, test, or educational environments.
The final verification confirmed that:
•	Apache was correctly configured to serve HTTPS traffic over port 443.
•	The SSL/TLS encryption was active, successfully securing data transmission.
•	The browser warning appeared only because the certificate was self-signed — not because encryption failed.
This project provided foundational knowledge for securing web services and laid the groundwork for integrating free and trusted SSL certificates (like Let’s Encrypt) in production environments.
Overall, it reinforces the importance of web security practices and prepares learners for advanced implementations involving automated certificate management, HTTPS redirection, and secure DevOps deployments.














