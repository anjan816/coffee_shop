# ☕ Coffee Shop CI/CD Pipeline Project

A complete end-to-end DevOps project demonstrating the deployment of a Coffee Shop Landing Page using **GitHub, Jenkins, Docker, Docker Hub, and AWS EC2, ElasticIP, Security Groups**.

This project automates the entire software delivery process, from source code management to containerized deployment.

## 🔥to run Project

http://YOUR-EC2-PUBLIC-IP

---

## 🌟 Features

- Automated CI/CD Pipeline using Jenkins
- HTML Validation Testing with HTMLHint
- Dockerized Application Deployment
- Docker Hub Integration
- AWS EC2 Deployment
- Nginx Web Server Hosting
- Automated Container Updates

---

## 🔄 CI/CD Workflow

```text
GitHub
   ↓
Jenkins Pipeline
   ↓
HTML Validation
   ↓
Docker Build
   ↓
Docker Hub Push
   ↓
AWS EC2 Deployment
   ↓
Live Website
```

---

## 🛠️ Technologies Used

- Git & GitHub
- Jenkins
- Docker
- Docker Hub
- AWS EC2
- Nginx
- HTML
- CSS
- Elastic IP
- Security Groups
---

## 📂 Project Structure

```text
coffee_shop/
│
├── src/
│   ├── index.html
│   ├── style.css
│   └── images/
│
├── Dockerfile
├── Jenkinsfile
└── README.md
```

---

## ⚙️ Jenkins Pipeline Stages

1. Checkout Source Code
2. HTML Validation Testing
3. Docker Image Build
4. Docker Hub Authentication
5. Docker Image Push
6. Automated Deployment to EC2

---

## 🐳 Docker Commands

### Build Image

```bash
docker build -t coffee_shop .
```

### Run Container

```bash
docker run -d --name coffee-container -p 80:80 coffee_shop
```

### Check Running Containers

```bash
docker ps
```

---

## 🚀 Future Improvements

- Multi-Architecture Docker Images (AMD64 & ARM64)
- HTTPS with SSL Certificate
- Kubernetes Deployment
- Monitoring with Prometheus & Grafana
- Automated Security Scanning

---

## 👨‍💻 Author

**Anjan Kumar k a**

- LinkedIn: https://www.linkedin.com/in/anjan-kumar-k-a-87a312204/
