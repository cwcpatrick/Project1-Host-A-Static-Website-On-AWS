![Alt text](/Host_a_Static_Website_on_AWS.png)

---

# 🌐 Host a Static Website on AWS

This project demonstrates how to host a **static HTML web application on AWS** using core **DevOps and cloud infrastructure components**. The setup ensures **high availability, scalability, fault tolerance, and security** by leveraging AWS services across multiple Availability Zones.

---

## 🚀 Project Overview

This deployment hosts a static web application on AWS EC2 instances within a secure, highly available architecture. The website is load-balanced, auto-scaled, and backed by AWS-managed services for networking, DNS, and monitoring.

A detailed **architecture diagram** and **deployment script** are included in this repository.

---

## 🧩 Architecture Components

1. **Virtual Private Cloud (VPC):**
   Configured with both public and private subnets across two different Availability Zones for redundancy and fault tolerance.

2. **Internet Gateway:**
   Enables internet access for instances in public subnets.

3. **Security Groups:**
   Serve as virtual firewalls controlling inbound and outbound traffic to instances.

4. **Multi-AZ Deployment:**
   Ensures high availability by distributing resources across two Availability Zones.

5. **Public Subnets:**
   Used for the **NAT Gateway** and **Application Load Balancer (ALB)**.

6. **Private Subnets:**
   Host the **web servers (EC2 instances)** for enhanced security.

7. **EC2 Instance Connect Endpoint:**
   Enables secure, browser-based SSH access to instances in both public and private subnets.

8. **NAT Gateway:**
   Allows instances in private subnets to securely access the internet (for updates and GitHub cloning).

9. **Application Load Balancer (ALB):**
   Distributes incoming traffic evenly across multiple EC2 instances within the Auto Scaling Group.

10. **Auto Scaling Group (ASG):**
    Automatically scales EC2 instances based on demand to ensure performance and availability.

11. **AWS Certificate Manager (ACM):**
    Manages SSL/TLS certificates to secure HTTPS communication.

12. **Simple Notification Service (SNS):**
    Sends alerts about Auto Scaling activities and instance health.

13. **Route 53:**
    Handles domain registration and DNS routing for the website.

14. **GitHub Integration:**
    Web application source code is hosted in this repository for version control and team collaboration.

---

## 🧰 Deployment Script

Below is the Bash script used to configure and deploy the web application on an EC2 instance:

```bash
#!/bin/bash
# Switch to root user
sudo su

# Update system packages
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Navigate to Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone project repository
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git

# Copy website files to Apache directory
cp -R host-a-static-website-on-aws/. /var/www/html/

# Remove cloned repository to clean up
rm -rf host-a-static-website-on-aws

# Enable Apache to start on boot
systemctl enable httpd

# Start Apache service
systemctl start httpd
```

---

## 🖼️ Architecture Diagram

Refer to the included **architecture diagram (architecture-diagram.png)** for a visual overview of the AWS setup.

---

## ⚙️ How It Works

1. The user accesses the registered domain via Route 53.
2. The request is routed through the Application Load Balancer.
3. The ALB distributes traffic evenly across EC2 instances in multiple AZs.
4. EC2 instances, hosted in private subnets, serve the static website using Apache.
5. The NAT Gateway allows instances in private subnets to access GitHub for updates.
6. Auto Scaling and SNS ensure continuous monitoring, scaling, and alerting.

---

## 🔒 Security Highlights

* EC2 instances run in private subnets (not directly exposed to the Internet).
* HTTPS enforced via AWS Certificate Manager.
* Security Groups restrict SSH and HTTP/HTTPS access to trusted sources.
* EC2 Instance Connect Endpoint enables secure SSH without direct public exposure.

---

## 🧑‍💻 Repository Contents

| File / Folder              | Description                        |
| -------------------------- | ---------------------------------- |
| `architecture-diagram.png` | AWS architecture reference diagram |
| `deploy.sh`                | EC2 deployment automation script   |
| `index.html`               | Sample static web page             |
| `README.md`                | Project documentation (this file)  |

---

## 🌍 Domain & DNS

The website’s domain name was registered and configured using **Amazon Route 53**, ensuring seamless and secure routing for global users.

---

## 📢 Notifications

AWS SNS sends email or SMS notifications about:

* Auto Scaling activities
* Instance launch/termination
* Health check alerts

---

## 🧾 Author

**Chad Williams**
Multi-Cloud Solutions Architect | AWS & Azure | DevOps | IaC | Security & Cost Optimization
🔗 [LinkedIn](https://www.linkedin.com/in/chadwilliams-dev)

---


