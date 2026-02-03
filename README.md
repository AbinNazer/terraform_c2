# Terraform EC2 Project – Abin Nazer

## Overview
This project demonstrates how to **provision an AWS EC2 instance using Terraform**.  
The goal was to automate cloud infrastructure creation, learn Terraform best practices, and deploy a simple server accessible via SSH.

Key achievements in this project:

- Provisioned an **EC2 instance** with Ubuntu 22.04.
- Used a **pre-existing EC2 key pair (`abinnazer`)** for secure SSH access.
- Configured Terraform to dynamically fetch the **latest AMI**, making the code region-independent.
- Selected **t3.micro**, which is AWS **Free Tier eligible**.
- Learned to handle **common Terraform & AWS errors** like IAM permissions, AMI availability, and SSH connectivity.
- Outputted the **public IP** for easy SSH access.

---

## What I Did and How

1. **Setup Terraform and AWS CLI**
   - Installed Terraform and AWS CLI locally.
   - Configured AWS CLI with IAM credentials.

2. **Created Terraform files**
   - `providers.tf` → Configured AWS provider with a region variable.
   - `variables.tf` → Defined variables for region, key name, and instance type.
   - `main.tf` → Created EC2 resource using a **dynamic data source for the latest Ubuntu 22.04 AMI**.
   - `outputs.tf` → Outputted the public IP of the instance for SSH access.

3. **Handled Key Pair**
   - Used existing key pair `abinnazer`.
   - Verified it existed in the correct AWS region.
   - Ensured `.pem` file was stored locally with correct permissions (`chmod 400`).

4. **Applied Terraform**
   - Ran `terraform init` to initialize the project.
   - Ran `terraform plan` to review changes.
   - Ran `terraform apply` to provision EC2.

5. **SSH Connection**
   - Connected to the EC2 instance via SSH using:
     ```bash
     ssh -i abinnazer.pem ubuntu@<PUBLIC_IP>
     ```
   - Learned to troubleshoot connection issues like:
     - Security group inbound rules (port 22 for SSH)
     - Network timeouts
     - Key file permissions

6. **Free Tier Considerations**
   - Changed instance type to `t3.micro` to stay within AWS Free Tier.
   - Learned that some instance types or AMIs are region-specific.

7. **Cleaning up**
   - Used `terraform destroy` to terminate the instance.
   - Optional: Remove local state to reset the project.

---

## Lessons Learned
- Terraform is **idempotent**, meaning repeated `apply` runs make no unnecessary changes.
- **IAM permissions** are crucial — without EC2 permissions, Terraform cannot create instances.
- **Region-specific resources** (AMIs, key pairs) can cause common errors; using dynamic data sources avoids this.
- Security best practices:
  - Never commit `.pem` keys to GitHub.
  - Limit SSH access in Security Groups to your IP.

---

## Folder Structure
terraform-ec2/
├── providers.tf # AWS provider configuration
├── variables.tf # Input variables for region, key name, instance type
├── main.tf # EC2 instance resource
├── outputs.tf # Public IP output
└── abinnazer.pem # Key pair (not committed to GitHub)

### Final Notes

This project is a hands-on demonstration of IaC (Infrastructure as Code) using Terraform, showcasing:

EC2 provisioning

Key pair management

Security Group configuration

Dynamic AMI selection

Terraform state management

---

## How to Use
1. Clone repository:
```bash
git clone <your-repo-url>
cd terraform-ec2
Initialize Terraform:

terraform init


Review plan:

terraform plan


Apply Terraform:

terraform apply


Type yes to confirm.

SSH into EC2:

chmod 400 abinnazer.pem
ssh -i abinnazer.pem ubuntu@<PUBLIC_IP>
