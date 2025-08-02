# manara-tech-finalproject

# My AWS Project

This project outlines the AWS architecture used for [Project 1: Scalable Web Application with ALB and Auto Scaling].

## 🎥 Project Walkthrough (Video)

For a full walkthrough and illustration of the infrastructure, watch the recorded video below:

[📺 Click here to watch the video](https://drive.google.com/file/d/1O4AJRxfBlWh8WS-8kcFittkJYycGSccZ/view?usp=sharing)

> The video includes an explanation of the architecture, deployment flow, and how the components interact.

## 📊 Architecture Diagram

![AWS Architecture Diagram](./assets/aws-architecture.png)

## 📄 Documentation

## 📐 Architecture Overview

This project sets up a scalable and secure AWS infrastructure to host a Docker-based web application connected to a MySQL database. The architecture follows best practices for high availability, fault tolerance, and automation.

### 🔧 Key Components

#### 🏗️ VPC and Networking
- **Custom VPC** with 4 subnets:
  - 2 Public Subnets
  - 2 Private Subnets
- **NAT Gateways**: Two NAT Gateways (one per public subnet) to provide internet access to private subnets.
- **Internet Gateway (IGW)**: Attached to the VPC to enable internet connectivity for public subnets.
- **Security Groups**: Used to control inbound and outbound access to all components.

#### 🗄️ Database Layer
- **Amazon RDS (MySQL)**:
  - Multi-AZ deployment with primary and standby instances for high availability.
  - Credentials managed via **AWS Secrets Manager**.
  - Data encrypted at rest using **AWS KMS**.

#### 🚀 Compute Layer
- **Amazon Machine Image (AMI)**:
  - Custom AMI created for the Dockerized web application.
- **Launch Template**:
  - Used to automate instance provisioning with the custom AMI.
- **Auto Scaling Group (ASG)**:
  - Automatically scales instances based on target tracking policy using **CloudWatch metrics**.
  - **SNS Notifications** configured to send email alerts on scaling events (e.g., instance termination or launch).
- **Application Load Balancer (ALB)**:
  - Internet-facing ALB to distribute incoming traffic across ASG instances.

---


## 📩 Notifications

All Auto Scaling activities (such as instance scale-up or termination) are monitored and pushed to an **Amazon SNS topic**, which sends email notifications for operational awareness.

---

## 🔐 Security

- **KMS Encryption** for sensitive data (RDS).
- **Secrets Manager** for secure credential storage.
- **Security Groups** for controlled access across services.

---

## ✅ Summary

This infrastructure provides:
- High availability and failover support (via Multi-AZ RDS and ASG).
- Secure and centralized credential management.
- Scalable compute resources using ASG and CloudWatch.
- Load balancing and internet exposure using ALB.
- Real-time alerts via SNS.
