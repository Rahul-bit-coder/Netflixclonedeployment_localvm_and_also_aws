# 🎬 Netflix Clone - CI/CD with Monitoring, Email & DevSecOps

A Netflix-style application with complete CI/CD pipeline, monitoring, alerting, and DevSecOps integration using tools like Jenkins, GitHub Actions, Prometheus, Grafana, Trivy, and more.

---

## 📖 Inspiration & Reference

This project is heavily inspired by the tutorial from [MrCloudBook](https://mrcloudbook.com/netflix-clone-ci-cd-with-monitoring-email-devsecops/).  
I followed the guide and applied the concepts step-by-step with my own modifications and enhancements.

---

## ⚙️ Tech Stack

| Layer          | Tool/Tech Used                   |
|----------------|----------------------------------|
| Frontend       | React.js                         |
| Backend        | Node.js, Express                 |
| CI/CD          | GitHub Actions + Jenkins         |
| Containerization| Docker                          |
| Monitoring     | Prometheus, Grafana              |
| Alerting       | SMTP Email via Grafana Alerts    |
| Security Scan  | Trivy                            |
| Reverse Proxy  | Nginx                            |

---

## 🛠️ Features Implemented

### ✅ Netflix Clone App
- Built using React and Node.js
- Dockerized for multi-stage builds
- Runs in isolated containers

### ✅ CI/CD Pipeline
- GitHub Actions for Continuous Integration
- Jenkins for Continuous Deployment
- Automatic builds on push to `main`

### ✅ DevSecOps: Trivy Integration

**Reference:** [Install Trivy - MrCloudBook Guide](https://mrcloudbook.com/netflix-clone-ci-cd-with-monitoring-email-devsecops/#2C_-_Install_Trivy)