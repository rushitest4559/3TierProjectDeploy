# 3TierProjectDeploy

This repository contains my 3-tier application deployment project on AWS. As a fresher, I designed and deployed a scalable web application using a 3-tier architecture, following the steps in [this blog post](https://medium.com/@aaloktrivedi/building-a-3-tier-web-application-architecture-with-aws-eb5981613e30).

## Project Overview

- **Architecture:** 3-tier (Presentation, Application, Database)
- **Cloud Platform:** AWS

## AWS Services Used

- **Amazon S3:** Hosted static frontend assets for high availability and durability.
- **Amazon CloudFront:** Delivered frontend content globally with low latency and improved performance.
- **Amazon EC2:** Deployed backend application servers using Auto Scaling Groups for scalability and reliability.
- **Amazon RDS:** Managed relational database for secure and scalable data storage.
- **Amazon VPC:** Created isolated network environments for secure communication between tiers.
- **Auto Scaling Groups:** Automatically scaled backend EC2 instances based on demand.
- **Amazon CloudWatch:** Monitored application and infrastructure metrics, set up alarms, and configured email notifications for critical events.
- **Amazon IAM:** Managed access and permissions for AWS resources.
- **Custom AMI:** Built and used a custom Amazon Machine Image with all required backend code and dependencies, eliminating the need for a NAT Gateway.

## Optimizations

- **Frontend Optimization:** Used S3 and CloudFront to host and deliver static assets, reducing costs and improving performance.
- **Backend Optimization:** Removed the NAT Gateway to save costs and enhance security. Instead, I created a custom AMI/template with all necessary packages and code, allowing backend instances to launch without internet access.
- **Monitoring & Alerts:** Integrated CloudWatch to monitor resource utilization and application health. Set up alarms to send email notifications for events such as high CPU usage or instance failures, ensuring proactive management.

## Reference

- [Building a 3-Tier Web Application Architecture with AWS](https://medium.com/@aaloktrivedi/building-a-3-tier-web-application-architecture-with-aws-eb5981613e30)

## How to Use

1. Clone this repository.
2. Follow the instructions in the referenced blog to deploy your own 3-tier application on AWS.
3. For backend deployment, use the provided template/AMI to launch instances without a NAT Gateway.
4. Configure CloudWatch alarms to monitor your resources and receive email notifications for important events.

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