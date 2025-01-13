# Hosting an HTML Website on an EC2 Instance

This project details the steps for hosting an HTML website on an Amazon EC2 instance using a 2-tier AWS network architecture.

## Steps

1. **Created a 2-tier AWS network VPC**
2. **Created and connected the NAT Gateways to the private Subnets**
3. **Created the Security Groups**
4. **Created Route tables**
5. **Created an ALB (Application Load Balancer) with Target Groups**
6. **Used an existing domain name in Route 53**
7. **Created a Record Set in Route 53**
8. **Registered for an SSL Certificate in AWS Certificate Manager (ACM)**
9. **Created an HTTPS (SSL) listener for the ALB**
10. **Created a Launch Template and Auto Scaling Group (ASG)**

---

## Deployment Script

The following Bash script automates the deployment of an HTML website on an EC2 instance:

```bash
#!/bin/bash

# Switch to the root user to gain full administrative privileges
sudo su

# Update all installed packages to their latest versions
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change the current working directory to the Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone the project GitHub repository to the current directory
git clone https://github.com/tifedaramola/html-website-on-ec2-instance.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R html-website-on-ec2-instance/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf html-website-on-ec2-instance

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

---

## Key Components and Tools Used
- **VPC (Virtual Private Cloud)**: For network segmentation.
- **NAT Gateway**: For secure internet access from private subnets.
- **Security Groups**: For controlling inbound and outbound traffic.
- **Route Tables**: For directing traffic within the VPC.
- **ALB (Application Load Balancer)**: For distributing incoming traffic.
- **Route 53**: For domain name management.
- **SSL Certificate Manager**: For HTTPS security.
- **Launch Template & ASG**: For scaling and managing EC2 instances.

This setup ensures a secure and scalable architecture for hosting a static website on an EC2 instance.

