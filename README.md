# Python App Deployment on AWS ECS with CI/CD

This project demonstrates how to deploy a simple Python (Flask) application to **AWS ECS (Fargate)** with an **Application Load Balancer** and a complete **CI/CD pipeline** using **GitHub Actions**.

---

## Features

- Flask-based sample Python app
- Docker containerization
- Deployment on AWS ECS (Fargate)
- Public access via Application Load Balancer (ALB)
- CI/CD with GitHub Actions:
  - Build and push Docker image
  - Deploy new version to ECS automatically

---

## Setup Guide

### 1. Prerequisites

- AWS account with IAM permissions for ECS, ECR, and CloudWatch
- GitHub repository
- AWS CLI installed (for local testing)
- Docker Hub or ECR repo created for image storage

---

### 2. Deploy to ECS (One-time Manual Steps)

- Create a Fargate-based ECS Cluster
- Define a Task Definition using:
  - Docker image: `yourdockerhubusername/flask-hello-ecs:latest`
  - Port: `80`
- Create a Service:
  - Load balanced with Application Load Balancer
  - At least 2 public subnets in different AZs
- Configure a Security Group:
  - Inbound HTTP (port 80) from 0.0.0.0/0
- Enable logs to CloudWatch

---

### 3. CI/CD with GitHub Actions

`.github/workflows/ci-cd.yml` handles:

- Docker login to Docker Hub
- Build and push image
- Trigger ECS deployment with latest image

> Secrets you need to set in GitHub:
```
DOCKER_USERNAME
DOCKER_PASSWORD
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_REGION
ECS_CLUSTER
ECS_SERVICE
```

---

## Docker Build & Run Locally

```bash
docker build -t flask-hello-ecs .
docker run -p 8080:80 flask-hello-ecs
# Access at http://localhost:8080
```

---

## Deployment Workflow Summary

1. Push code to `main`
2. GitHub Actions builds Docker image
3. Image pushed to Docker Hub (or ECR)
4. ECS Service is updated with new image (`--force-new-deployment`)
5. Load Balancer routes traffic to new task

---

## Future Enhancements

- Add Prometheus + Grafana for ECS monitoring
- Use Terraform to provision ECS, ALB, and networking
- Replace `latest` tag with versioned tags and task definition automation

---

## Screenshot

- Are under screenshot dir.

---

## Author

**Punit Pawar**  
DevOps Deployment on AWS ECS with GitHub Actions

---
