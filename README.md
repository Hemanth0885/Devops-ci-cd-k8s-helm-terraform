# Devops-ci-cd-k8s-helm-terraform
End-to-end DevOps CI/CD pipeline using Jenkins, Docker, Kubernetes (EKS), Helm, and Terraform

## Overview
This repository demonstrates a complete DevOps workflow using
CI/CD pipelines, containerization, Kubernetes orchestration, Helm charts,
and infrastructure automation with Terraform.

 Note:
This is a personal demo project created for learning and showcasing
DevOps practices. No production or client-specific code is included.

## Tech Stack
- Jenkins, GitHub Actions
- Docker
- Kubernetes (EKS), Helm
- Terraform
- AWS (EC2, VPC, IAM, EKS, CloudWatch)
- Bash

## CI/CD Flow
1. Code commit triggers Jenkins pipeline
2. Build and validate application
3. Docker image is created and pushed to registry(used dockerhub)
4. Application is deployed to Kubernetes using Helm
5. Rolling updates ensure zero-downtime deployment


## Infrastructure Automation
AWS infrastructure including VPC, IAM, and EKS is provisioned using Terraform,
ensuring consistent and repeatable environments.


## Kubernetes & Helm
Helm charts are used to manage application manifests and environment-specific
values, simplifying deployments and rollbacks.


## Notes
This project focuses on DevOps automation and deployment strategies rather
than application business logic.
