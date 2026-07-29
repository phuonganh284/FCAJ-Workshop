---
title : "Clean up"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---
### Resource Cleanup and Decommissioning

Following the successful completion of the deployment, testing, and evaluation phases for the maintenance management system, all cloud infrastructure resources were systematically decommissioned and cleaned up in accordance with standard operational procedures to optimize costs and eliminate unexpected billing risks on the AWS account.

* **Storage Sanitization and Repository Deletion (Amazon S3):** Performed a complete purge of all experimental data files, images, and maintenance documents stored within the S3 Bucket (`tracker-maintenance-images-123`), followed by the deletion of the bucket configuration to thoroughly clear the object storage space.

* **Server Termination and Privilege Revocation (EC2 & IAM):** Executed the termination of the Amazon EC2 virtual server instance to release computational resources, while revoking and deleting the IAM Roles and security policies previously provisioned under the Principle of Least Privilege.

* **Database and Network Infrastructure Teardown (RDS & VPC):** Deleted the Amazon RDS relational database instance (`tracker-maintenance-db`) to secure sensitive structured data, subsequently detaching the Internet Gateway, clearing routing tables, and deleting the Tracker-VPC configuration to restore the network environment to its original state.

* **Monitoring Configuration Purge (Amazon CloudWatch):** Erased the CloudWatch Log Groups that recorded the runtime activity logs of the Spring Boot application, finalizing the complete decommissioning and retrieval of the experimental cloud infrastructure ecosystem.