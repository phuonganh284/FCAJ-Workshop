---
title: "Proposal"
date: 2026-07-26
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

## Tracker Maintenance – Equipment Maintenance Management System on AWS
### Secure Operational Solution with Multi-tier Cloud Architecture and Layered Security

### 1. Executive Summary

Tracker Maintenance is a modern multi-tier application designed to manage equipment maintenance operations, deployed on Amazon Web Services (AWS). The user interface (Frontend) is developed using React, while the core business logic (Backend) is powered by Spring Boot (Java 21), integrated with a secure relational database hosted within an isolated private network infrastructure.

### 2. Objectives

The core objectives of the Tracker Maintenance project focus on optimizing management workflows and maximizing information security:

- Build a stable cloud infrastructure with clear segmentation between public and private secure subnets.
- Deploy a robust Spring Boot application server incorporating layered security standards and strict access control mechanisms.
- Optimize the processing efficiency of maintenance files and multimedia assets through integrated Amazon S3 object storage.
- Establish a centralized monitoring and log aggregation system to ensure comprehensive system observability.

### 3. Problem Statement

- **Current Status:** Traditional management systems often struggle with access permission controls, pose data security risks, and frequently experience bottlenecks when handling heavy file uploads directly through central servers.
- **Solution:** Tracker Maintenance leverages Amazon VPC to isolate its database layer. The backend application (Spring Boot) is securely deployed on Amazon EC2, combined with Amazon S3 object storage and Amazon CloudWatch for monitoring.
- **Benefits:** Delivers a highly available, securely fortified system from the network layer down to the application layer, while providing an intuitive management interface and seamless experience for technical teams.

### 4. System Architecture

The entire infrastructure is deployed in the ap-southeast-2 (Sydney) AWS region with a clearly segregated network structure.

**Technologies Used:**

- **Frontend:** React / Tailwind CSS.
- **Backend:** Spring Boot (Java 21).
- **Database:** Amazon RDS (PostgreSQL).

**Core AWS Services:**

- **Amazon VPC:** Establishes a private networking space, segmented into Public Subnets (hosting EC2) and Private Subnets (hosting RDS).
- **Amazon EC2:** Virtual server running the Spring Boot API application and core business logic.
- **Amazon RDS:** Relational database storing system information and maintenance records.
- **Amazon S3:** Secure object storage repository for system images and technical documentation.
- **Amazon CloudWatch:** Centralized monitoring service capturing runtime application logs.
- **Route 53 & ACM / Private CA:** Manages domain name resolution and secure SSL/TLS communication certificates.
- **Amazon Bedrock:** Integrates artificial intelligence to support maintenance data analytics.

![System Architecture](/images/AWS_Architecture.png)

**Main Data Flows:**

- **Business Processing Flow:** Users submit requests through the frontend interface, traversing the public network tier to reach the Spring Boot API server on EC2, and subsequently querying data securely from the RDS database within the private network zone.
- **File Management Flow:** The Spring Boot server processes and interacts directly with the Amazon S3 storage repository utilizing secured IAM Role permissions.

### 5. Technical Implementation

The development team divides specific tasks to ensure steady project progression:

- **Application Development (Frontend & Backend):** Building the user interface using React and developing business APIs with Spring Boot.
- **AWS Infrastructure Provisioning:** Designing the VPC network topology, configuring stringent Security Groups, and deploying RDS and EC2 instances.
- **Security and Monitoring:** Configuring IAM policies following the Principle of Least Privilege and integrating CloudWatch Logs for observability.

### 6. Implementation Roadmap

The project roadmap is structured into distinct sequential phases:

- **Phase 1:** Initializing source code repositories, database design, and basic UI wireframing.
- **Phase 2:** Developing backend business logic with Spring Boot and establishing local database connectivity.
- **Phase 3:** Provisioning AWS network infrastructure (VPC, Subnets, Security Groups) and deploying the RDS database.
- **Phase 4:** Deploying the application onto Amazon EC2, configuring S3 storage, finalizing CloudWatch monitoring, and executing comprehensive integration testing.

### 7. Risk Assessment

- **Unauthorized Database Access Risk:** Completely eliminated through VPC network design, isolating Amazon RDS within a Private Subnet with no direct public internet exposure.
- **Credential Leakage Risk:** Meticulously mitigated via secure environment variable configurations and strict adherence to minimum IAM privilege principles.

### 8. Expected Outcomes

Successfully deploy a secure, stable, and high-performance Tracker Maintenance system on AWS. The project demonstrates core proficiencies in multi-tier architectural design and the practical application of modern cloud computing services to real-world maintenance management challenges.