Study Log - August 2, 2025


---

#  Terraform Intro (Day 16 Study Notes)

---

## Terraform

Terraform is an **open-source Infrastructure as Code (IaC)** tool developed by **HashiCorp** that allows you to **provision, manage, and version cloud infrastructure** using configuration files.

---

##  HCL Syntax (HashiCorp Configuration Language)

### Basic Structure

```hcl
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

###  Key Components of HCL

| Component  | Description                                                 |
| ---------- | ----------------------------------------------------------- |
| `provider` | Specifies the cloud/platform to use (AWS, Azure, GCP, etc.) |
| `resource` | Defines the infrastructure components (EC2, S3, VPC)        |
| `variable` | Declares input values                                       |
| `output`   | Displays values after provisioning                          |
| `module`   | Reusable Terraform code block                               |

---

## Providers

### What are Providers?

* Plugins that interact with **APIs** (e.g., AWS, Azure, GCP).
* Required to create and manage resources.

### Example:

```hcl
provider "aws" {
  region = "ap-south-1"
}
```

Terraform downloads the AWS provider plugin during `terraform init`.

---

## Resources

### What is a Resource?

* The **infrastructure component** managed by Terraform.
* Every resource has a **type** and a **name**.

### Example:

```hcl
resource "aws_s3_bucket" "my_bucket" {
  bucket = "amith-bucket-001"
  acl    = "private"
}
```

Here, `aws_s3_bucket` is the **resource type**, `my_bucket` is the **resource name**.

---

## Terraform State Management

###  What is Terraform State?

* A file (`terraform.tfstate`) that stores **current infrastructure metadata**.
* Helps Terraform **know what it created**.

###  State File Characteristics:

* JSON format
* Tracks real-world resources
* Required for all Terraform operations

### Security Tip:

* State may contain **sensitive info** like passwords → never expose it publicly.

---

## Remote Backends

###  What is a Backend?

* Controls where Terraform **stores the state**.

###  Local vs Remote:

| Type   | Stored Where?                        |
| ------ | ------------------------------------ |
| Local  | `terraform.tfstate` on local machine |
| Remote | AWS S3, Terraform Cloud, etc.        |

###  Example: S3 Backend

```hcl
terraform {
  backend "s3" {
    bucket = "my-tf-backend"
    key    = "global/s3/terraform.tfstate"
    region = "ap-south-1"
  }
}
```

---

##  State Locking

### What is State Locking?

* Prevents multiple users from changing infrastructure **at the same time**.

### Why Locking Matters?

Without it, concurrent changes can lead to **corruption or conflicts** in state.

###  Used With:

* S3 backend + DynamoDB for state locking.

### Example:

```hcl
terraform {
  backend "s3" {
    bucket         = "my-tf-backend"
    key            = "terraform.tfstate"
    region         = "ap-south-1"
    dynamodb_table = "terraform-locks"
    encrypt        = true
  }
}
```

---

##  Common Terraform Commands

| Command              | Description                               |
| -------------------- | ----------------------------------------- |
| `terraform init`     | Initialize project, download providers    |
| `terraform plan`     | Show what Terraform will do               |
| `terraform apply`    | Apply changes and create/update infra     |
| `terraform destroy`  | Delete all resources managed by Terraform |
| `terraform state`    | Inspect or modify state file manually     |
| `terraform validate` | Check syntax errors                       |
| `terraform fmt`      | Auto-format the code                      |

---

##  Best Practices

* Always use **version control (Git)** with Terraform code.
* Use **modules** for reusability.
* Use **variables** for dynamic configuration.
* Protect and **encrypt the state file**.
* Enable **state locking** using DynamoDB (if using S3 backend).
* Do **`terraform plan`** before every apply.

---


