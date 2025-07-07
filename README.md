# AWS

## 🌐 What is AWS?

provides on-demand cloud services like servers, databases, storage, networking, machine learning, and more — all accessible over the internet. <br>
Instead of buying and maintaining your own physical hardware, you rent what you need from AWS and scale as you go.
---

# 🧱 Key features:
Compute	EC2 (virtual servers), Lambda (serverless) - Run applications and processes <br>
Storage	S3 (object storage), EBS, Glacier	Store and back up data <br>
Databases	RDS, DynamoDB, Aurora	Managed relational & NoSQL databases <br>
Networking	VPC, CloudFront, Route 53	Connect and distribute resources <br>
Security	IAM, KMS, Cognito	Manage access and encryption <br>

# 📁 Who Uses AWS?:
Startups, Enterprises, Government agencies, Developers & data scientists

# ✅ Benefits of AWS:
Pay-as-you-go pricing  <br>
Highly scalable <br>
Global infrastructure <br>
High availability & security <br>
Wide range of services <br>

## 📝 AWS - First steps
Step 1: Create an AWS Account: https://aws.amazon.com <br>
Step 2: Fill information - enter your details <br>
Step 3: Choose account typ (Personal or Professional) <br>
Step 4: Enter billing info <br>
Step 5: Verify your identity <br>
Step 6: Choose support plan - Basic Support (free) <br>
Step 7: Sign in to the AWS Management Console - ROOT Account <br>
Step 8: Enable MFA <br>
Step 9: Never use root for daily work <br>


# 🧱 Create a separate AWS user/account with full admin access 
AWS root user has unrestricted access - Billing card, etc. <br>
Root user use only for critical tasks <br>

Step 1: Sign in using the root user to AWS Console : [https://aws.amazon.com](https://aws.amazon.com/console/) <br>
Step 2: Open IAM (Identity and Access Management) <br>
Step 3: In the IAM dashboard, Users - Add users <br>
Step 4: Assign Permissions - Attach policies directly - AdministratorAcces <br>
Step 5: Sign In as the New Admin User - AWS will give you a direct sing-in URL. <br>
Step 6: Enable MFA <br>
Step 7: Never use root for daily work


# Deploying Node.js on AWS EC2
Step 1: Create EC2 instance - I am using Ubuntu Free Tier <>
Step 2: In security section - leave all settings and add PORT 3000 from your IP address <br>
Step 3: Create KEY pair and download - .PEM or .PPK format <br>
Step 4: Launch instance <br>
Step 5: Wait for turning on instance and connect with your generated keypair <br>
Step 6: Every instance has own public IP - use that for connection for example from Putty - Windows

![Snímek obrazovky 2025-07-07 191231](https://github.com/user-attachments/assets/2a4a72df-e87a-46ca-9be9-f911e2b85571)

Step 7: Setup EC2 Instance - Download and install updates
```
sudo apt update
sudo apt upgrade
```
Step 8: Install Node.js
```
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt-get install -y nodejs
```
Step 9: Upload your node.JS file for run to Ubuntu EC2 Instance
```
You can use tool: WinSCP - Windows
On Mac, Linux rsync - rsync -avz /path/to/local/file username@remote_host:/path/to/remote/destination/
-a: Archive mode (preserves permissions, timestamps, etc.)
-v: Verbose output (optional but helpful)
-z: Compress file during transfer (optional, good for large files)
/path/to/local/file: Path to the file you're uploading
```
Step 10: Run in terminal 
```
node example.js
```
![Snímek obrazovky 2025-07-07 192723](https://github.com/user-attachments/assets/61fcae76-99be-4b65-901b-57d947aa0df2)

Step 10: Set your service like System Service - for running on background 
```
sudo nano /etc/systemd/system/myapp.service

[Unit]
Description=Simple Node.js Servioce
After=network.target multi-user.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/JS
ExecStart=/usr/bin/node /home/ubuntu/JS/example.js
Restart=on-failure
Environment=NODE_ENV=production
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=myapp

[Install]
WantedBy=multi-user.target
```
Step 11: Reload systemd and start your service
```
sudo systemctl daemon-reload
sudo systemctl enable myapp.service
sudo systemctl start myapp.service
sudo systemctl status myapp.service
```
If your Node.js app need DB you can install it very easy
```
sudo apt install mysql-server
sudo systemctl start mysql
sudo systemctl enable mysql
sudo mysql -u root

CREATE DATABASE my_app;
CREATE USER 'my_app_user'@'localhost' IDENTIFIED WITH mysql_native_password BY 'MyFirstPass123!';
GRANT ALL PRIVILEGES ON my_app.* TO 'my_app_user'@'localhost';
```





