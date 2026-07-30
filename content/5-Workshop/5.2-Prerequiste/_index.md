---
title : "Prerequisite"
date : 2026-07-26
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

### Prerequisites

### AWS Account and Access (AWS IAM & AWS CLI)

The system requires an active AWS account. To follow the **Principle of Least Privilege**, the project uses an **IAM user account** instead of the AWS Root account for daily administration and development tasks. The IAM user is also used to generate access credentials for connecting to AWS services through the AWS CLI.

#### Step 1: Generate an Access Key

Sign in to the **AWS Management Console** using the IAM user account and navigate to:

**IAM → Users → Security credentials**

Under the **Access keys** section, select **Create access key**, choose **Command Line Interface (CLI)** as the use case, acknowledge the recommendations, and complete the creation process.

AWS will generate:

- **Access Key ID**
- **Secret Access Key**

Download the generated **.csv** file and store it securely.

<div style="text-align: center; margin: 20px 0;">

<img src="/FCAJ-Workshop/images/iam.png" alt="iam" width="1000" />
<div style="font-weight: bold; margin-top: 8px; color: #555;">Figure 2. Security credentials page of the IAM user in AWS IAM.</div>

</div>

#### Step 2: Configure AWS CLI

Open **Terminal** (Linux/macOS) or **PowerShell** (Windows) and execute:

```bash
aws configure
```

Enter the following information:

- **AWS Access Key ID**
- **AWS Secret Access Key**
- **Default region name:** `ap-southeast-2`
- **Default output format:** `json`

The configuration files will be stored automatically in:

- **Linux/macOS:** `~/.aws/`
- **Windows:** `%USERPROFILE%\.aws\`

> **Note:** The **IAM → Security credentials → Access keys** page is used to generate authentication credentials for AWS CLI access.

---

### Local Development Environment

To develop, build, and deploy the Spring Boot application, the local machine should have the following software installed:

- **Java Development Kit (JDK) 21** for application development.
- **Maven or Gradle** for dependency management and project builds.
- **Git** for source code management and version control.

The project should also prepare the required environment variables to securely store configuration values, including:

- Database connection information.
- Amazon S3 configuration.
- Amazon CloudWatch configuration.

Sensitive configuration files should never be committed to the Git repository. Configure the `.gitignore` file properly before pushing source code.

---

### AWS Region

According to the project architecture, all AWS resources are deployed in the following Region:

```text
ap-southeast-2 (Asia Pacific – Sydney)
```

Using a single AWS Region ensures that services such as **Amazon VPC**, **Amazon EC2**, **Amazon RDS**, **Amazon S3**, and **Amazon CloudWatch** can communicate efficiently while minimizing latency and avoiding deployment issues caused by cross-region resources.