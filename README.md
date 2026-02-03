# Terraform EC2 Provisioning Project

## Overview
This project uses **Terraform** to provision an **AWS EC2 instance** with the following features:

- Automatically selects the **latest Ubuntu 22.04 AMI** for the region.
- Uses the **existing EC2 key pair** `abinnazer` for SSH access.
- Deploys a **t3.micro instance** (AWS Free Tier eligible).
- Outputs the **public IP** for SSH connection.
- Easy to destroy all resources to avoid AWS charges.

---

## Folder Structure
terraform-ec2/
├── providers.tf # AWS provider configuration
├── variables.tf # Variables for region, instance type, and key
├── main.tf # EC2 instance resource definition
├── outputs.tf # Outputs public IP of EC2
└── abinnazer.pem # Your EC2 key pair

---

## Prerequisites

1. AWS account with **EC2 permissions** (`AmazonEC2FullAccess` policy recommended)
2. AWS CLI installed and configured:

```bash
aws configure
AWS Access Key ID

---

AWS Secret Access Key

Default region (e.g., us-east-1)

Output format (json)

Terraform installed (v1.5+ recommended)

Key pair file abinnazer.pem available locally

Quick Start
1️⃣ Initialize Terraform
bash
Copy code
terraform init
2️⃣ Preview the plan
bash
Copy code
terraform plan
3️⃣ Apply Terraform
bash
Copy code
terraform apply
Type yes when prompted.
This will create the EC2 instance.

4️⃣ Output Public IP
After apply completes, Terraform outputs the public IP:

bash
Copy code
instance_public_ip = "YOUR_PUBLIC_IP"
5️⃣ SSH into the EC2 instance
bash
Copy code
chmod 400 abinnazer.pem
ssh -i abinnazer.pem ubuntu@YOUR_PUBLIC_IP
Destroy Resources
To avoid AWS charges, destroy everything:

bash
Copy code
terraform destroy
Type yes when prompted.

Optional: Remove Terraform local state if needed:

bash
Copy code
rm -rf terraform.tfstate terraform.tfstate.backup .terraform/
Notes
Security: Do not commit .pem files to GitHub.

Region-Specific: AMI IDs are dynamically retrieved, so the project works in any region.

Free Tier: Use t3.micro instance type to remain within AWS Free Tier limits.
