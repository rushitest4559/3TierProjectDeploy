# 3TierProjectDeploy

This repository contains my 3-tier application deployment project on AWS. As a fresher, I designed and deployed a scalable web application using a 3-tier architecture, following the steps in [this blog post](https://medium.com/@aaloktrivedi/building-a-3-tier-web-application-architecture-with-aws-eb5981613e30).

## Project Overview

- **Architecture:** 3-tier (Presentation, Application, Database)
- **Cloud Platform:** AWS

## AWS Services Used

- **Amazon EC2:** Deployed backend application servers using Auto Scaling Groups for scalability and reliability.
- **Amazon RDS:** Managed relational database for secure and scalable data storage.
- **Amazon VPC:** Created isolated network environments for secure communication between tiers.
- **Auto Scaling Groups:** Automatically scaled backend EC2 instances based on demand.
- **Amazon CloudWatch:** Monitored application and infrastructure metrics, set up alarms, and configured email notifications for critical events.
- **Amazon IAM:** Managed access and permissions for AWS resources.
- **Custom AMI:** Built and used a custom Amazon Machine Image with all required backend code and dependencies, eliminating the need for a NAT Gateway.

## Cost Optimizations

- **Frontend Hosting:** For further cost optimization and performance, the frontend can be hosted using Amazon S3 and delivered via CloudFront CDN. This approach eliminates server maintenance and reduces costs compared to EC2-based hosting.
- **Backend Optimization:** Removed the NAT Gateway to save costs and enhance security. Instead, I created a custom AMI/template with all necessary packages and code, allowing backend instances to launch without internet access.
- **Monitoring & Alerts:** Integrated CloudWatch to monitor resource utilization and application health. Set up alarms to send email notifications for events such as high CPU usage or instance failures, ensuring proactive management.

## Challenges Faced & Solutions

During the deployment of this 3-tier architecture, I encountered several challenges, especially with connectivity between the frontend, backend, and database layers. The main issues were related to misconfigured Security Groups and Network ACLs (NACLs), which blocked communication between the tiers.

- **Frontend to Backend Connectivity:**  
  Initially, the frontend (hosted on an EC2 instance) could not reach the backend EC2 instances due to restrictive inbound rules in the backend's Security Group. I resolved this by updating the Security Group to allow HTTP/HTTPS traffic from the frontend instance's IP or subnet.

- **Backend to Database Connectivity:**  
  The backend EC2 instances were unable to connect to the Amazon RDS database. This was caused by missing inbound rules in the RDS Security Group and overly restrictive NACLs. I fixed this by:
  - Allowing inbound MySQL/PostgreSQL traffic (port 3306/5432) from the backend subnet in the RDS Security Group.
  - Adjusting NACLs to permit traffic between backend and database subnets.

- **General Troubleshooting:**  
  I used AWS CloudWatch logs and VPC Flow Logs to identify blocked connections and verify that traffic was flowing correctly after making changes.

These experiences helped me understand the importance of properly configuring Security Groups and NACLs for secure and reliable communication in a cloud environment.

## Best Practices Followed

Throughout the deployment, I adhered to AWS best practices to ensure clarity, maintainability, and security:

- **Meaningful Naming Conventions:**  
  I assigned clear, descriptive names to all AWS resources, including subnets, NACLs, security groups, instance templates, and route tables. This made it easier to identify and manage resources, especially when troubleshooting connectivity issues.

- **Resource Organization:**  
  Grouped related resources logically (e.g., frontend, backend, database subnets and security groups) to simplify management and auditing.

- **Security Group & NACL Configuration:**  
  Carefully configured security groups and NACLs, understanding that security groups are stateful and NACLs are stateless. This helped me set correct inbound and outbound rules, and avoid common connectivity errors.

- **Route Table Associations:**  
  Ensured route tables were properly associated with the correct subnets, and followed naming conventions for easy identification.

- **Jump Server Access:**  
  Faced challenges accessing backend instances securely. I resolved this by setting up a jump server (bastion host) and updating security group rules to allow SSH access only from trusted IPs.

- **Learning from Architecture Diagrams:**  
  Most of my troubleshooting was guided by understanding the architecture diagram provided in the referenced blog. This helped me visualize network flows and correctly configure resource associations.

By following these best practices, I minimized errors and improved the overall reliability and security of my AWS deployment.

## Step-by-Step Deployment Approach (Less Error-Prone)

Based on my experience, the most reliable way to deploy a 3-tier architecture on AWS is to start by drawing and understanding the architecture diagram in your notebook. This visual reference is crucial for planning and troubleshooting.

### 1. VPC & Networking Setup
- **Create a VPC** with a /16 CIDR block for flexibility.
- **Create Subnets, NAT, and Internet Gateway manually:**  
  Doing this step-by-step helps you understand each component and assign meaningful names for clarity.
- **Create 2 NACLs:**  
  - Public NACL for public-facing resources  
  - Private NACL for backend/database resources  
  Set rules according to the diagram.
- **Create 4 Security Groups:**  
  - Frontend SG  
  - Backend SG  
  - RDS SG  
  - Jump Server SG  
  Set inbound/outbound rules as per the architecture diagram.
- **Create Internet Gateway** and attach it to the VPC.
- **Create 6 Subnets** (/24 CIDR, 3 public + 3 private for high availability) with clear, descriptive names.
- **Create 2 Route Tables:**  
  - One for public subnets  
  - One for private subnets  
  Set routes and associate them with the correct subnets.

> **Note:** NAT Gateway is not required due to the custom AMI/template approach.

### 2. Instance Preparation & AMI Creation
- **Launch 2 temporary EC2 instances** (one for frontend, one for backend).
- **Deploy your code** and install all required packages on these instances.
- **Create AMIs and launch templates** from these instances.
- **Delete the temporary instances and AMIs** after templates are created (only templates are needed for Auto Scaling Groups).

### 3. Auto Scaling Groups & Database
- **Create 2 Auto Scaling Groups:**  
  - One for frontend  
  - One for backend  
  Use the launch templates and assign the correct security groups.
- **Create RDS Database:**  
  - Allow access from anywhere initially  
  - Create the database with the same name as your backend expects  
  - Update your backend template with the RDS endpoint.

### 4. Final Steps
- **Access your application:**  
  Copy the frontend load balancer domain name and open it in your browser to verify deployment.

---

## Key Skills Demonstrated

- Cloud architecture design and deployment on AWS
- Cost optimization and security best practices
- Automated scaling and high availability
- Infrastructure monitoring and alerting
- End-to-end deployment of a production-ready web application

---

Feel free to update this README with more details about your application, configuration, or deployment steps.

---

**Note:** This project demonstrates my ability to design, optimize, and deploy cloud infrastructure using AWS best practices. I am actively seeking opportunities to apply my skills in a professional environment. If you are looking for a motivated and skilled cloud engineer, please feel free to contact me.