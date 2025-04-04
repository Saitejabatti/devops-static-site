# CI/CD Pipeline with Jenkins, Docker, and AWS

This project showcases a fully automated CI/CD pipeline built using:

- **Jenkins** (for automation and orchestration)
- **GitHub** (for source code management)
- **Docker** (for containerization)
- **Docker Hub** (for image registry)
- **AWS EC2** (for deployment server)

## 🚀 Features

- Automatic build trigger from GitHub using webhooks
- Jenkins pipeline for building and pushing Docker images
- Dockerized Nginx static site deployment
- Live deployment on EC2 instance
- Elastic IP ensures consistent server access

## 🔧 Tools Used

- Jenkins (Declarative Pipeline)
- Git & GitHub
- Docker & Docker Hub
- AWS EC2
- Webhooks

## 🧱 Pipeline Workflow

1. Code pushed to GitHub
2. Webhook triggers Jenkins pipeline
3. Docker image is built and pushed to Docker Hub
4. EC2 instance pulls the latest image
5. Container runs and serves the static website

## 🌐 Access

Site is accessible via [Elastic IP](http://<YOUR_ELASTIC_IP>)

## 📂 Folder Structure
. ├── Dockerfile ├── index.html ├── Jenkinsfile └── README.md

## ✅ How to Use

1. Fork or clone this repo.
2. Configure Jenkins and Docker on your EC2.
3. Set up GitHub webhook.
4. Run the Jenkins pipeline.

---

🛠 Developed with ❤️ as part of DevOps learning journey.
