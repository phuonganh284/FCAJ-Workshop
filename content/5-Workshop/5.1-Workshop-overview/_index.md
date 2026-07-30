---
title : "Introduction"
date : 2026-07-26
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

### Cloud Web Infrastructure Deployment and System Security Setup

<div style="text-align: center; margin: 20px 0;">

  <img src="/FCAJ-Workshop/images/AWS_Architecture.png" alt="event" width="1000" />
  
  <div style="font-weight: bold; margin-top: 8px; color: #555;">Figure 1. Overall architecture of the network infrastructure and AWS service integration for the Tracker Maintenance project.</div>
</div>

<br>

### Overview

This lab documents the complete process of building, configuring, and testing the cloud infrastructure for the **Tracker Maintenance System** project.

The deployment focuses on implementing a multi-tier web architecture on AWS in the **ap-southeast-2 (Sydney)** Region with clearly separated network components and secure data processing flows, including:

* Establishing an **Amazon Virtual Private Cloud (VPC)** within a single Availability Zone, divided into a **Public Subnet** (to receive Internet traffic) and a **Private Subnet** (to isolate and protect the Amazon RDS database).
* Deploying the **Spring Boot** backend application on **Amazon EC2** to process business logic and provide RESTful APIs for the frontend application.
* Connecting the application server to **Amazon RDS (PostgreSQL)** located inside the Private Subnet to ensure secure and reliable database access.
* Storing maintenance images and technical documents in **Amazon S3**, allowing the application to securely upload, manage, and retrieve files.
* Managing access permissions through **AWS Identity and Access Management (IAM)** while using **Amazon CloudWatch** to centralize application logs, monitor system performance, and track infrastructure health.

Through this deployment, the **Tracker Maintenance** system provides a secure, reliable, and scalable cloud infrastructure while following AWS best practices for networking, storage, monitoring, and security.