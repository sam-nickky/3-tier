#DevOps Assignment: 3-Tier Web Application Using Docker + Kubernetes


The goal is to build and deploy a 3-tier web application using Docker and Kubernetes, demonstrating core DevOps concepts like containerization, orchestration. This solution uses AWS EC2 for hosting a lightweight K3s Kubernetes cluster and Helm/Kubectl for deployment.3

# Stack Used
Frontend: Nginx serving a static HTML file

Backend: Python Flask application (Simple Shopping API)

Database: MySQL

Containerization: Docker

Orchestration: Kubernetes (via K3s)

Infrastructure: AWS EC2

IaC Tools: Kubernetes YAML Manifests (can be extended to Helm)

# Infrastructure Setup
Launched AWS EC2 Instance

OS: Ubuntu 22.04

Opened security group ports: 30080, 30001, 80, 3306, 5000

#Installed Dependencies on EC2

# Install Docker
sudo apt update && sudo apt install -y docker.io
sudo systemctl enable docker && sudo systemctl start docker

# Install K3s 
curl -sfL https://get.k3s.io | sh 

# Directory Structure

root@ip-172-31-40-219:~/3-tier# tree
.
├── backend
│   ├── Dockerfile
│   ├── app.py
│   └── requirements.txt
├── database
│   ├── Dockerfile
│   ├── cm.yml
│   └── init.sql
├── frontend
│   ├── Dockerfile
│   ├── index.html
│   └── nginx.conf
└── k8s
    ├── backend-deploy.yaml
    ├── db-deploy.yaml
    ├── deploy_db.yaml
    └── frontend-deploy.yaml

5 directories, 13 files
![app](https://github.com/user-attachments/assets/5a293a74-507e-450f-880b-4be5dd0b86cc)

# Docker Image Build & Push
Images were built and pushed to Docker Hub:

# Kubernetes Deployment
Navigate to the k8s/ directory for deployment manifests:



#  Accessing the Application
Access the application via:

Frontend: http://<EC2_PUBLIC_IP>:30080

Backend API: http://<EC2_PUBLIC_IP>:30001/products

MySQL DB: Accessible within cluster or via kubectl port-forward
