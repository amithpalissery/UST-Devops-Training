Study Log - August 4, 2025


Terraform Modules Guide: VPC + EC2 Provisioning
===============================================

Introduction to Terraform Modules
------------------------------------
- Terraform modules are reusable configuration packages.
- Benefits:
  -  Reusability: Write once, use anywhere.
  -  Organization: Group related resources.
  -  Encapsulation: Hide complexity.
  -  Versioning & Collaboration.

Prerequisites
-----------------
- Terraform 1.0+ installed
- AWS CLI configured
- IAM permissions for EC2 & VPC
- Basic AWS knowledge

Required IAM Permissions
---------------------------
{
    "Effect": "Allow",
    "Action": ["ec2:*", "vpc:*"],
    "Resource": "*"
}

Project Structure
--------------------
project-root/
├── main.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
└── modules/
    ├── network/
    │   ├── main.tf, variables.tf, outputs.tf
    └── compute/
        ├── main.tf, variables.tf, outputs.tf

Network Module Highlights
----------------------------
- Creates VPC, subnets, route tables, security groups
- Inputs: VPC CIDR, subnet CIDRs, AZs, env, project_name
- Outputs: VPC ID, subnet IDs, SG ID

Compute Module Highlights
----------------------------
- Launches EC2 instances using Launch Templates
- Inputs: VPC/Subnet/SecurityGroup IDs, AMI, instance_type, count
- Outputs: Instance IDs, IPs, Launch Template ID

Root Module (main.tf)
------------------------
- Declares provider (AWS) & versions
- Calls network & compute modules with required inputs

terraform.tfvars (Example Values)
-----------------------------------
project_name     = "my-web-app"
environment      = "dev"
aws_region       = "us-west-2"
key_pair_name    = "my-key-pair"
instance_type    = "t3.micro"
instance_count   = 2

Provisioning Steps
---------------------
1. Create directories and copy files
2. Create Key Pair: `aws ec2 create-key-pair ...`
3. Update `terraform.tfvars` with actual values
4. Initialize: `terraform init`
5. Plan: `terraform plan`
6. Apply: `terraform apply`
7. Verify Outputs & Access EC2

Destroy Resources
---------------------
- Plan destruction: `terraform plan -destroy`
- Destroy: `terraform destroy`

Best Practices
-----------------
- Single responsibility modules
- Secure resources (SSH, SGs)
- Use Remote State (S3 + DynamoDB)
- Version control (Git)
- Separate environments using workspaces

backend.tf (Example)
-----------------------
terraform {
  backend "s3" {
    bucket         = "your-bucket"
    key            = "terraform.tfstate"
    region         = "us-west-2"
    dynamodb_table = "terraform-lock-table"
    encrypt        = true
  }
}

Debugging & AWS CLI
-----------------------
- Debug: `TF_LOG=DEBUG terraform apply`
- Format: `terraform fmt -recursive`
- Validate: `terraform validate`
- Show state: `terraform show`
- AWS CLI Examples:
  - List VPCs: `aws ec2 describe-vpcs`
  - List instances: `aws ec2 describe-instances`
