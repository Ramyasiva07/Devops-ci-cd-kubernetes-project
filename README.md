# DevOps CI/CD Kubernetes Monitoring Project

## Project Overview

This project demonstrates a complete DevOps workflow including:

- Source Code Management using GitHub
- CI/CD Automation using Jenkins
- Containerization using Docker
- Kubernetes Deployment using Minikube
- Monitoring using Prometheus & Grafana
- GitHub Webhook Integration using Ngrok

The project automates application build, Docker image creation, deployment, and monitoring in a Kubernetes environment.

---

## Architecture Flow

1. Developer pushes code to GitHub
2. GitHub Webhook triggers Jenkins pipeline
3. Jenkins builds Docker image
4. Docker image pushed to DockerHub
5. Kubernetes deploys updated application
6. Prometheus collects Kubernetes metrics
7. Grafana visualizes monitoring dashboards

---

## Tools & Technologies

- GitHub
- Jenkins
- Docker
- DockerHub
- Kubernetes (Minikube)
- Prometheus
- Grafana
- Helm
- Ngrok
- Python (Flask App)

---

## Jenkins & Webhook Setup

### Start Jenkins

Open:
http://localhost:8080

### Expose Jenkins using Ngrok

ngrok http 8080

Add webhook in GitHub:

https://<ngrok-url>/github-webhook/

GitHub webhook automatically triggers Jenkins pipeline on every code push.

---

## Docker Workflow

### Build Docker Image

docker build -t ramyasiva07/portfolio:latest .

### Push Image to DockerHub

docker push ramyasiva07/portfolio:latest

DockerHub credentials were securely configured inside Jenkins.

---

## Kubernetes Deployment

### Start Minikube

minikube start

### Deploy Application

kubectl apply -f k8s/

### Verify Resources

kubectl get pods

kubectl get svc

### Restart Deployment

kubectl rollout restart deployment portfolio

### Access Application

minikube service portfolio-service

Application is exposed using Kubernetes Service for external access.

---

## Monitoring Setup using Prometheus & Grafana

### Install Monitoring Stack

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo update

helm install monitoring prometheus-community/kube-prometheus-stack

---

## Access Grafana Dashboard

kubectl port-forward svc/monitoring-grafana 3000:80

Open:
http://localhost:3000

### Login

Username:
admin

### Get Password

kubectl get secret monitoring-grafana -o jsonpath="{.data.admin-password}" | base64 --decode

---

## Access Prometheus UI

kubectl port-forward svc/monitoring-kube-prometheus-prometheus 9090:9090

Open:
http://localhost:9090

Prometheus was used to:
- Run PromQL queries
- View raw metrics
- Debug monitoring data

---

## Grafana Dashboard Metrics

### Pod Metrics

kube_pod_info{pod=~"portfolio.*"}

### CPU Usage

rate(container_cpu_usage_seconds_total{pod=~"portfolio.*"}[5m])

### Memory Usage

container_memory_usage_bytes{pod=~"portfolio.*"}

### Pod Count

count(kube_pod_info{pod=~"portfolio.*"})

---

## Screenshots

- Jenkins Pipeline Success
- DockerHub Image Push
- Kubernetes Pods Running
- Kubernetes Services
- Grafana Dashboard
- CPU Usage Graph
- Memory Usage Graph
- Pod Count Metrics
- Final Portfolio Application

---

## Restart Workflow

After system restart:

minikube start

kubectl apply -f k8s/

minikube service portfolio-service

Start Jenkins and Ngrok again.

---

## Key Learning

- Built automated CI/CD pipeline using Jenkins
- Integrated GitHub Webhook automation
- Containerized application using Docker
- Deployed application into Kubernetes cluster
- Implemented monitoring using Prometheus
- Visualized metrics using Grafana dashboards
- Managed Kubernetes deployments and services

---

## Future Improvements

- Deploy on AWS EKS
- Use LoadBalancer instead of NodePort
- Configure Ingress Controller
- Implement centralized logging

---

## Conclusion

This project demonstrates a complete real-time DevOps workflow including CI/CD automation, containerization, Kubernetes deployment, webhook integration, and monitoring using modern DevOps tools.
