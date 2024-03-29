# Hosting a Static Website on AWS

This project demonstrates the process of hosting a static HTML web application on AWS. Below is a detailed README outlining the configuration and deployment steps involved in setting up the infrastructure and deploying the web application.

## Project Overview
The project utilizes various AWS services and resources to host a static website, ensuring scalability, fault tolerance, and security.

## Infrastructure Configuration
1. **Virtual Private Cloud (VPC)**:
   - Configured with public and private subnets across two availability zones for enhanced availability and fault tolerance.

2. **Internet Gateway**:
   - Deployed to facilitate connectivity between VPC instances and the wider Internet.

3. **Security Groups**:
   - Utilized as a network firewall mechanism to control traffic to EC2 instances.

4. **Availability Zones**:
   - Utilized two availability zones to enhance system reliability and fault tolerance.

5. **Public Subnets**:
   - Used for infrastructure components like NAT Gateway and Application Load Balancer.

6. **EC2 Instance Connect Endpoint**:
   - Implemented for secure connections to assets within both public and private subnets.

7. **Private Subnets**:
   - Positioned web servers (EC2 instances) within private subnets for enhanced security.

8. **NAT Gateway**:
   - Enabled instances in private subnets to access the Internet.

## Deployment Process
1. **EC2 Instance Setup**:
   - Installed Apache HTTP Server and Git on EC2 instances using provided scripts.
   - Cloned the project GitHub repository containing the static website files.
   - Copied files to the Apache web root directory and cleaned up unnecessary files.

2. **Load Balancer and Auto Scaling**:
   - Utilized an Application Load Balancer (ALB) and a target group to evenly distribute web traffic.
   - Employed Auto Scaling Groups to automatically manage EC2 instances, ensuring availability, scalability, fault tolerance, and elasticity.

3. **Version Control and Collaboration**:
   - Stored web files on GitHub for version control and collaboration.

4. **Security Measures**:
   - Secured application communications using a Certificate Manager.
   - Configured Simple Notification Service (SNS) to alert about activities within the Auto Scaling Group.

5. **Domain Setup**:
   - Registered the domain name and set up DNS records using Route 53.

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
git clone https://github.com/femiotolorin/host-a-static-website-on-aws.git
# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/
# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws
# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd
# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

## Conclusion
This project successfully demonstrates the deployment of a static website on AWS, utilizing various services and resources to ensure availability, scalability, and security. It provides a reliable foundation for hosting static web applications in a cloud environment.
