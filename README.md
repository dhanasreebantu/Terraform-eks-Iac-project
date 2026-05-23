# Production-Grade AWS EKS Infrastructure using Terraform

## Project Overview

This project demonstrates how to build a production-style AWS infrastructure using Terraform (Infrastructure as Code).

The infrastructure includes:

* AWS VPC
* Public Subnet
* Private Subnet for Kubernetes (EKS)
* Private Subnet for Database
* Internet Gateway
* NAT Gateway
* Public & Private Route Tables
* Amazon EKS Cluster
* IAM Role and Policies

---

# Architecture Diagram

```text
                           Internet
                               |
                        +---------------+
                        | Internet GW   |
                        +---------------+
                               |
                     ----------------------
                     |                    |
             Public Route Table     Private Route Table
                     |                    |
             +---------------+     +---------------+
             | Public Subnet |     | Private Subnet|
             |               |     |   (EKS)       |
             +---------------+     +---------------+
                     |                    |
               NAT Gateway         Amazon EKS Cluster
                     |
             +----------------+
             | Database Subnet|
             +----------------+
```

---

# Technologies Used

* Terraform
* AWS
* Amazon EKS
* Kubernetes
* AWS VPC
* NAT Gateway
* IAM
* Git & GitHub

---

# Project Structure

```bash
terraform-eks-project/
│
├── provider.tf
├── variables.tf
├── vpc.tf
├── subnets.tf
├── nat.tf
├── route_tables.tf
├── eks.tf
├── outputs.tf
├── terraform.tfvars
├── .gitignore
└── README.md
```

---

# Prerequisites

Before starting, install the following tools:

## Terraform

[https://developer.hashicorp.com/terraform/downloads](https://developer.hashicorp.com/terraform/downloads)

## AWS CLI

[https://aws.amazon.com/cli/](https://aws.amazon.com/cli/)

## kubectl

[https://kubernetes.io/docs/tasks/tools/](https://kubernetes.io/docs/tasks/tools/)

---

# AWS Configuration

Configure AWS CLI:

```bash
aws configure
```

Provide:

```bash
AWS Access Key ID
AWS Secret Access Key
Region = ap-south-1
Output format = json
```

---

# Step-by-Step Implementation

## Step 1 — Create Provider Configuration

File: `provider.tf`

Configured AWS provider and region.

---

## Step 2 — Create Variables

File: `variables.tf`

Defined:

* AWS Region
* VPC CIDR Block

---

## Step 3 — Create VPC

File: `vpc.tf`

Created:

* Main VPC
* DNS support enabled

---

## Step 4 — Create Subnets

File: `subnets.tf`

Created:

### Public Subnet

* Used for NAT Gateway
* Internet accessible

### Private Subnet

* Used for EKS Cluster
* Secure internal communication

### Database Subnet

* Dedicated private subnet for database

---

## Step 5 — Create Internet Gateway

File: `nat.tf`

Created Internet Gateway for public internet access.

---

## Step 6 — Create NAT Gateway

File: `nat.tf`

Created:

* Elastic IP
* NAT Gateway

Purpose:

Allows private subnet resources to access the internet securely.

---

## Step 7 — Configure Route Tables

File: `route_tables.tf`

Created:

### Public Route Table

* Connected to Internet Gateway

### Private Route Table

* Connected to NAT Gateway

Associated route tables with subnets.

---

## Step 8 — Configure IAM Role for EKS

File: `eks.tf`

Created:

* IAM Role
* EKS IAM Policies

---

## Step 9 — Create Amazon EKS Cluster

File: `eks.tf`

Created Kubernetes cluster using:

* Public Subnet
* Private Subnet

---

# Terraform Commands

## Initialize Terraform

```bash
terraform init
```

---

## Validate Configuration

```bash
terraform validate
```

---

## Preview Infrastructure

```bash
terraform plan
```

---

## Create Infrastructure

```bash
terraform apply
```

Type:

```bash
yes
```

---

## Destroy Infrastructure

```bash
terraform destroy
```

---

# Configure kubectl

Connect kubectl to EKS Cluster:

```bash
aws eks update-kubeconfig --region ap-south-1 --name main-eks-cluster
```

Verify:

```bash
kubectl get nodes
```

---

# Security Best Practices

* Used private subnet for Kubernetes nodes
* Used NAT Gateway for secure outbound access
* Separate subnet for database
* IAM-based authentication
* Infrastructure managed using Terraform

---

# GitHub Best Practices

Added `.gitignore` to avoid uploading:

```gitignore
.terraform/
*.tfstate
*.tfstate.*
terraform.tfvars
```

---

# Future Improvements

The project can be enhanced with:

* EKS Managed Node Groups
* RDS Database
* S3 Remote Backend
* DynamoDB State Locking
* GitHub Actions CI/CD
* Helm Charts
* ArgoCD GitOps
* Prometheus & Grafana Monitoring
* Bastion Host
* Auto Scaling

---

# Learning Outcomes

Through this project, I learned:

* Infrastructure as Code using Terraform
* AWS Networking Concepts
* Public and Private Subnet Architecture
* NAT Gateway and Route Tables
* Amazon EKS Setup
* IAM Role Management
* Terraform Deployment Lifecycle
* Git and GitHub Integration

---

# Conclusion

This project demonstrates a real-world AWS infrastructure setup using Terraform and Kubernetes. It follows industry-standard networking practices and provides a strong foundation for DevOps, Cloud, and Platform Engineering roles.

---

