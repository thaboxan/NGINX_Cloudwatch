# NGINX_Cloudwatch

# Week 7 - ECS Fargate + ALB + CloudWatch Dashboard

This Terraform project deploys an **nginx container** on **Amazon ECS (Fargate)**, fronted by an **Application Load Balancer (ALB)**, and sets up a **CloudWatch dashboard** to monitor CPU and memory utilization.

---

## **Architecture Overview**

* **VPC** with 2 public subnets (for ALB and ECS tasks).
* **Application Load Balancer** to route HTTP traffic to ECS tasks.
* **ECS Cluster** running an nginx container using Fargate.
* **CloudWatch Dashboard** with CPU & Memory graphs.

---

## **Prerequisites**

* [Terraform](https://developer.hashicorp.com/terraform/downloads) v1.0+
* AWS account with CLI credentials configured (`aws configure`)
* Permissions to create VPC, ECS, ALB, IAM roles, and CloudWatch resources.

---

## **Deployment Steps**

### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd week7
```

### 2. Initialize Terraform

```bash
terraform init
```

### 3. Review and Apply

```bash
terraform plan
terraform apply
```

Type `yes` when prompted.

### 4. Get Your App URL

After deployment, Terraform outputs:

```bash
app_url = "http://<your-load-balancer-dns>"
```

Visit this URL in your browser to see the nginx welcome page.

You can also run:

```bash
terraform output app_url
```

---

## **Viewing the CloudWatch Dashboard**

### From the AWS Console:

1. Go to **CloudWatch → Dashboards**.
2. Find the dashboard named `<app_name>-dashboard` (default: `nginx-app-dashboard`).
3. Open it to see CPU and Memory utilization graphs for your ECS service.

---

## **Simulating Load**

You can generate traffic to see metrics change in CloudWatch.

### Apache Bench (ab)

**Install:**

* Amazon Linux: `sudo yum install -y httpd-tools`

**Run:**

```bash
ab -n 5000 -c 50 http://<your-load-balancer-dns>/
```

## **Destroying the Environment**

When finished:

```bash
terraform destroy
```

Type `yes` when prompted.

---


## **Outputs**

* **`app_url`**: Public URL for the nginx app.
* **`ecs_cluster_name`**: ECS cluster name.
* **`cloudwatch_dashboard`**: Dashboard name in AWS CloudWatch.

---

## **Notes**


* Metrics in CloudWatch may take 1–2 minutes to update.
* Adjust `var.app_name` in `terraform.tfvars` or directly in the variable block to deploy under a different name.

---

## **Screenshots**

**1. ECS Service Running NGINX**
<img width="1920" height="1080" alt="Screenshot (15)" src="https://github.com/user-attachments/assets/fc92ea50-2ca4-4a48-91b7-45703d9a8e06" />

**2. CloudWatch Dashboard Overview**
<img width="1920" height="1080" alt="Screenshot (18)" src="https://github.com/user-attachments/assets/d7434472-d5bf-488b-873d-fa8d41f093a0" />

**3. CPU Utilization Graph**
<img width="1920" height="1080" alt="Screenshot (17)" src="https://github.com/user-attachments/assets/100e947d-d8af-4008-9242-71300ed8afdc" />

**4. Memory Utilization Graph**
<img width="1920" height="1080" alt="Screenshot (16)" src="https://github.com/user-attachments/assets/075d3d06-cdf2-4ea9-854b-2a00fd4adc2a" />

