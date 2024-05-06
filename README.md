# Host a Static Website on AWS

In this Cloud Computing project, I hosted a static web application on Amazon Web Services, utilizing the resources and services listed below. Additionally, the reference diagram and scripts used are provided below.

## Services and resources used

1. Configured a Virtual Private Cloud (VPC) with both public and private subnets across two different availability zones.
2. Deployed an Internet Gateway to facilitate connectivity between VPC instances and the wider Internet.
3. Established Security Groups as a network firewall mechanism.
4. Leveraged two Availability Zones to enhance system reliability and fault tolerance.
5. Utilized Public Subnets for infrastructure components like the NAT Gateway and Application Load Balancer.
6. Implemented EC2 Instance Connect Endpoint for secure connections to assets within both public and private subnets.
7. Positioned web servers (EC2 instances) within Private Subnets for enhanced security.
8. Enabled instances in both the private Application and Data subnets to access the Internet via the NAT Gateway.
9. Hosted the website on EC2 Instances.
10. Employed an Application Load Balancer and a target group for evenly distributing web traffic to an Auto Scaling Group of EC2 instances across multiple Availability Zones.
11. Utilized an Auto Scaling Group to automatically manage EC2 instances, ensuring website availability, scalability, fault tolerance, and elasticity.
12. Stored web files on GitHub for version control and collaboration.
13. Configured Simple Notification Service (SNS) to alert about activities within the Auto Scaling Group.

## Deployment Script
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
git clone https://github.com/guilhermefgonc/aws-static-website.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R aws-static-website/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf aws-static-website

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd 

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

## Reference Architecture
![arch](/architecture.png)
