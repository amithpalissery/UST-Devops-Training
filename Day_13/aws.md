Study Log - July 30, 2025

# **Day 13: AWS Cloud Introduction & Networking Stack**

---

1. **AWS Cloud Overview**

### What is AWS?

* AWS (Amazon Web Services) is a secure cloud services platform offering compute power, storage, networking, databases, analytics, machine learning, IoT, and more.
* Enables organizations to scale and grow quickly, cost-effectively, and securely.

### Core AWS Services Categories:

| Category     | Services                                 |
| ------------ | ---------------------------------------- |
| Compute      | EC2, Lambda, ECS, EKS, Elastic Beanstalk |
| Storage      | S3, EBS, EFS, Glacier                    |
| Database     | RDS, DynamoDB, Aurora                    |
| Networking   | VPC, Route 53, ELB, CloudFront           |
| Security     | IAM, KMS, Cognito, Security Groups       |
| DevOps/CI-CD | CodePipeline, CodeBuild, CloudWatch      |
| AI/ML        | SageMaker, Rekognition, Comprehend       |

---

2. **AWS Global Infrastructure**

* **Region:** A geographical area (e.g., `us-east-1`)
* **Availability Zone (AZ):** A data center (or multiple) in a region (e.g., `us-east-1a`)
* **Edge Location:** Global CDN edge servers used by services like CloudFront

---

3. **Networking in AWS**

### What is VPC (Virtual Private Cloud)?

* A **logically isolated network** defined by the user within AWS.
* Components include:

  * **Subnets**
  * **Route Tables**
  * **Internet Gateway / NAT Gateway**
  * **Security Groups**
  * **Network ACLs**

###  CIDR Block:

* IP range defined for VPC: e.g., `10.0.0.0/16` (supports 65,536 IPs)

---

4. **Subnets**

* Sub-segment of the VPC’s IP range.
* **Public Subnet:**

  * Has route to Internet Gateway
  * Hosts EC2s or Bastion Hosts that need internet
* **Private Subnet:**

  * No direct internet access
  * Typically used for databases, backend services

---

5. **Routing**

* **Route Table:** Controls traffic direction for subnets
* **Internet Gateway (IGW):** Enables internet access for public subnets
* **NAT Gateway / NAT Instance:** Allows private subnets to initiate outbound traffic to the internet

---

6. **Bastion Host**

* A special-purpose EC2 instance in a **public subnet**
* Used to securely **SSH into EC2s in private subnets**
* Inbound port 22 open only for trusted IPs

---

7. **IP Addressing in AWS**

| Type           | Description                                                  |
| -------------- | ------------------------------------------------------------ |
| **Private IP** | Assigned from subnet IP range, used internally               |
| **Public IP**  | Auto-assigned (changes on restart unless Elastic IP is used) |
| **Elastic IP** | Static public IP you can attach to EC2                       |

---
