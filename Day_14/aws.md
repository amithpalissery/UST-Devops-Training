Study Log - July 31, 2025

# **Day 14: EC2, Container Services, Security & Cost Saving**

---

1. **Amazon EC2 (Elastic Compute Cloud)**

* Virtual machines (instances) in the cloud
* Choose:

  * **AMI (Amazon Machine Image):** OS + preinstalled apps
  * **Instance Type:** vCPU, memory (e.g., t2.micro, m5.large)
  * **Key Pair:** For SSH login
  * **EBS Volumes:** Storage block

### EC2 Lifecycle:

* Start → Stop → Terminate
* Terminating an instance deletes attached volumes (unless flagged otherwise)

### EC2 Dashboard Features:

* Launch Wizard
* Monitor metrics (CPU, network, disk I/O)
* Add/Remove volumes
* Assign Elastic IPs
* Attach IAM roles

---

2. **Security Group**

* Acts as a virtual firewall attached to EC2 or other resources
* **Stateful**: Return traffic is automatically allowed
* Configure **Inbound** and **Outbound** rules

  * By default:

    * All outbound allowed
    * No inbound allowed (must be manually added)

### Example Rules:

| Direction | Protocol | Port | Source    |
| --------- | -------- | ---- | --------- |
| Inbound   | TCP      | 22   | My IP     |
| Inbound   | TCP      | 80   | 0.0.0.0/0 |
| Outbound  | All      | All  | 0.0.0.0/0 |

---

3. **Container Services**

### **Amazon ECS (Elastic Container Service)**

* Orchestration for Docker containers
* **Launch Types:**

  * EC2 Launch: You manage the infrastructure
  * Fargate Launch: Fully serverless (no EC2 to manage)

###  **Amazon EKS (Elastic Kubernetes Service)**

* Fully managed Kubernetes control plane
* Scales automatically
* Use AWS CLI, eksctl, or Console to manage clusters
* Worker nodes run on EC2 or Fargate

---

4. **AWS Cost Optimization**

| Strategy                        | Description                                           |
| ------------------------------- | ----------------------------------------------------- |
| **Use Free Tier**               | t2.micro free for 12 months                           |
| **Stop EC2 when not in use**    | Avoid being charged hourly                            |
| **Use Spot Instances**          | 70-90% cheaper than On-Demand                         |
| **Right-size instances**        | Choose optimal size based on usage                    |
| **Billing Alarms (CloudWatch)** | Get notified when usage exceeds threshold             |
| **S3 Lifecycle Rules**          | Transition infrequently accessed objects              |
| **Reserved Instances**          | Long-term savings (1-year or 3-year commitment)       |
| **Instance Scheduler**          | Automate start/stop of instances during working hours |

---

