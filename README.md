# DevOps Assignment: 3-Tier Web Application Using Docker + Kubernetes


The goal is to build and deploy a 3-tier web application using Docker and Kubernetes, demonstrating core DevOps concepts like containerization, orchestration. This solution uses AWS EC2 for hosting a lightweight K3s Kubernetes cluster and Helm/Kubectl for deployment.3

# Stack Used:
Frontend: Nginx serving a static HTML file

Backend: Python Flask application (Simple Shopping API)

Database: MySQL

Containerization: Docker

Orchestration: Kubernetes (via K3s)

Infrastructure: AWS EC2

IaC Tools: Kubernetes YAML Manifests (can be extended to Helm)

# Infrastructure Setup:

Launched AWS EC2 Instance

OS: Ubuntu 22.04

Opened security group ports: 30080, 30001, 80, 3306, 5000

#Installed Dependencies on EC2

# Install Docker:
sudo apt update && sudo apt install -y docker.io
sudo systemctl enable docker && sudo systemctl start docker

# Install K3s :

curl -sfL https://get.k3s.io | sh 

# Directory Structure:

![app](https://github.com/user-attachments/assets/5a293a74-507e-450f-880b-4be5dd0b86cc)

# Docker Image Build & Push:

Images were built and pushed to Docker Hub:

    # Frontend
    docker build -t <dockerhub-username>/frontend:latest frontend
    docker push <dockerhub-username>/frontend:latest

    # Backend
    docker build -t <dockerhub-username>/backend:latest backend
    docker push <dockerhub-username>/backend:latest

    # DB
    docker build -t <dockerhub-username>/db:latest db
    docker push <dockerhub-username>/db:latest

# Kubernetes Deployment:

Navigate to the k8s/ directory for deployment manifests:

    kubectl apply -f k8s/

#  Accessing the Application:

Access the application via:

Frontend: http://<EC2_PUBLIC_IP>:30080
![Screenshot (30)](https://github.com/user-attachments/assets/4c785c30-4289-4d2f-aea5-85a94e64161f)


Backend API: http://<EC2_PUBLIC_IP>:30001/products
![Screenshot (25)](https://github.com/user-attachments/assets/98ce2c5c-8c83-4151-ad37-b3f644575afb)


MySQL DB: Accessible within cluster or via kubectl port-forward
