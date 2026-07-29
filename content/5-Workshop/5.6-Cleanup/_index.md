---
title : "Difficulties & Development Direction"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---
### Challenges & Future Development

### Challenges Encountered

* **Network Security Configuration and Internal Authorization (Security Groups & IAM):** During the process of establishing a closed, secure connection between the Spring Boot application server (housed in the Public Subnet) and the Amazon RDS database (housed in the Private Subnet), the team encountered initial obstacles regarding misconfigured Inbound rules within Security Groups, resulting in connection refusals. Troubleshooting through CloudWatch Logs enabled the team to correctly adjust communication ports and source identifiers.

* **File Security Policy Conflicts (Bucket Policy & IAM Roles):** When configuring security for the `tracker-maintenance-images-123` storage repository, enforcing overly strict Public Access Block policies temporarily triggered write access denial exceptions (**Access Denied**) from the backend server. The team had to review the entire IAM Role permission mechanism and refine security policies to ensure compliance with the Principle of Least Privilege while maintaining smooth operations.

* **Payload Uniformity and Data Validation Issues:** Incoming file upload requests and maintenance data payloads occasionally suffered from missing parameters or structural deviations caused by network transmission disruptions. This initially generated exceptions in the Spring Boot business logic layer. The team resolved this by implementing rigorous data input validation mechanisms (`@Valid`, Bean Validation) alongside centralized exception handling blocks (Global Exception Handler).

### Future Directions

* **Infrastructure as Code (IaC):** Transition the entire manual provisioning process on the AWS Management Console (VPC, Subnets, EC2, RDS, S3, IAM) to centralized infrastructure management using Terraform or AWS CloudFormation. This will standardize deployment environments, simplify infrastructure replication, and improve version control.

* **Advanced Artificial Intelligence Integration (Amazon Bedrock):** Expand the system’s intelligent analysis capabilities by leveraging foundation models on Amazon Bedrock to support automated equipment fault diagnosis based on historical maintenance records and generate technical solution recommendations.

* **Unified Management and Monitoring Dashboard (Fleet Dashboard):** Integrate CloudWatch log streams and database information into a centralized administration dashboard that provides performance metrics, infrastructure health monitoring, and real-time maintenance activities for more efficient system operation.