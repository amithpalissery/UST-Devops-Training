Study Log - August 1, 2025
---

#  **Day 15: AWS EKS and ECS – Container Orchestration**

---

##  **What Are Containers?**

* Containers package your application code, libraries, and dependencies into a **single lightweight unit**.
* Run consistently across different environments.
* Use **Docker** or **containerd** to build and run containers.

---

##  **AWS Container Services Overview**

| Service     | Description                                                       |
| ----------- | ----------------------------------------------------------------- |
| **ECS**     | AWS-managed container orchestration using Docker (AWS native)     |
| **EKS**     | AWS-managed Kubernetes (open-source container orchestration)      |
| **Fargate** | Serverless compute engine for containers (works with ECS and EKS) |

---

##  **Amazon ECS (Elastic Container Service)**

###  What is ECS?

* A **fully managed container orchestration service** from AWS.
* Runs Docker containers.
* Integrates with EC2 or Fargate for compute.

###  ECS Components:

| Component           | Description                                              |
| ------------------- | -------------------------------------------------------- |
| **Task Definition** | Blueprint for running containers (like Docker Compose)   |
| **Task**            | Running instance of a Task Definition                    |
| **Service**         | Maintains desired count of Tasks, enables load balancing |
| **Cluster**         | Logical grouping of Tasks/Services                       |

---

### ECS Launch Types:

| Launch Type | Description                                            |
| ----------- | ------------------------------------------------------ |
| **EC2**     | You manage the EC2 instances (container host machines) |
| **Fargate** | AWS manages the infrastructure (serverless containers) |

---

###  ECS Workflow:

1. Create **Task Definition**
2. Define **Service** with desired task count
3. Choose **Launch Type** (EC2 or Fargate)
4. Define **Cluster**
5. Deploy and monitor containers

---

## ☸ **Amazon EKS (Elastic Kubernetes Service)**

###  What is EKS?

* A **fully managed Kubernetes** control plane by AWS.
* Lets you run Kubernetes workloads on AWS infrastructure.
* Supports **standard kubectl and Helm** tools.

---

###  EKS Architecture:

| Component         | Description                                  |
| ----------------- | -------------------------------------------- |
| **Control Plane** | Managed by AWS (API server, etcd, scheduler) |
| **Worker Nodes**  | Run your Kubernetes pods (on EC2 or Fargate) |
| **VPC**           | Network in which the cluster resides         |
| **Node Groups**   | Set of worker nodes managed as a group       |

---

### 🔧 EKS Workflow:

1. Create EKS Cluster (via Console, CLI, or `eksctl`)
2. Configure `kubectl` to connect to EKS
3. Deploy worker nodes using EC2 or Fargate
4. Apply Kubernetes manifests (Deployments, Services, etc.)

---

##  **ECS vs EKS – Quick Comparison**

| Feature              | ECS                       | EKS                          |
| -------------------- | ------------------------- | ---------------------------- |
| Orchestration Engine | AWS native                | Kubernetes                   |
| Learning Curve       | Easier (fully abstracted) | Steeper (K8s complexity)     |
| Flexibility          | Less flexible             | Highly flexible              |
| Ecosystem            | Tied to AWS               | Vendor-agnostic (K8s)        |
| Community            | AWS supported             | Open-source global community |
| Customization        | Low                       | High                         |

---

##  **When to Use What?**

| Use Case                                   | Best Option        |
| ------------------------------------------ | ------------------ |
| Simple microservices on AWS                | ECS with Fargate   |
| Need advanced orchestration or portability | EKS                |
| Already using Kubernetes                   | EKS                |
| Minimal DevOps effort                      | ECS with Fargate   |
| Full control over K8s workloads            | EKS with EC2 nodes |

---

##  Key Concepts to Remember

| Concept         | ECS                        | EKS                                 |
| --------------- | -------------------------- | ----------------------------------- |
| Task            | ECS container workload     | Pod (Kubernetes container)          |
| Task Definition | Blueprint of containers    | Deployment YAML file                |
| Cluster         | Logical container group    | Kubernetes cluster                  |
| Service         | Runs desired task count    | Kubernetes Service resource         |
| Autoscaling     | Integrated with CloudWatch | Kubernetes HPA / Cluster Autoscaler |

---

##  Security Considerations

* Use **IAM Roles for Tasks** (ECS) and **IAM for Service Accounts (IRSA)** (EKS)
* Integrate with **AWS CloudWatch**, **GuardDuty**, **ECR scanning**, and **VPC security groups**

---

##  Monitoring & Logging

| Tool               | ECS        | EKS            |
| ------------------ | ---------- | -------------- |
| CloudWatch Logs    | ✅          | ✅              |
| Container Insights | ✅          | ✅              |
| Prometheus/Grafana | ❌ (manual) | ✅ (K8s native) |
| AWS X-Ray          | ✅          | ✅              |

---

##  CI/CD with ECS & EKS

* Use **GitHub Actions**, **AWS CodePipeline**, or **Jenkins** to:

  * Build Docker images
  * Push to **Amazon ECR**
  * Deploy to ECS/EKS via `kubectl`, `eksctl`, or **ECS CLI**

---

##  Sample CLI Tools

| Tool      | Purpose                    |
| --------- | -------------------------- |
| `aws ecs` | Manage ECS services        |
| `ecs-cli` | Simplified ECS usage       |
| `eksctl`  | Create/manage EKS clusters |
| `kubectl` | Deploy to Kubernetes       |
| `helm`    | Kubernetes package manager |

---

##  Sample ECS Task Definition Snippet:

```json
{
  "family": "my-ecs-task",
  "containerDefinitions": [
    {
      "name": "app",
      "image": "my-app-image",
      "memory": 512,
      "cpu": 256,
      "essential": true,
      "portMappings": [
        {
          "containerPort": 8080,
          "hostPort": 8080
        }
      ]
    }
  ]
}
```

---

##  Summary Table

| Feature           | ECS                           | EKS                            |
| ----------------- | ----------------------------- | ------------------------------ |
| Use Case          | Simple, AWS-focused workloads | Complex, multi-cloud workloads |
| Setup Complexity  | Low                           | High                           |
| Deployment Units  | Tasks                         | Pods                           |
| Networking        | Integrated with VPC           | CNI plugin for K8s networking  |
| Serverless Option | Fargate                       | Fargate                        |
| Best for          | Simpler microservices         | Full Kubernetes control        |

---


