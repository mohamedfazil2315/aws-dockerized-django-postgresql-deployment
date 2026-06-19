# Dockerized Django Application with PostgreSQL on AWS EC2

Project Overview

This project demonstrates the deployment of a production-ready Django web application using Docker containers on AWS EC2 instances.

The application tier and database tier are hosted on separate EC2 instances, following a Two-Tier Architecture approach.

SQLite was replaced with PostgreSQL to achieve better scalability, reliability, and production readiness.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# ARCHITECTURE DIAGRAM 
                     
                     Internet
                         │
                         ▼
                ┌─────────────────┐
                │ Django EC2      │
                │ Ubuntu          │
                │ Docker          │
                │ Django App      │
                └────────┬────────┘
                         │
               Port 5432 Allowed
                 Security Group
                         │
                         ▼
                ┌─────────────────┐
                │ PostgreSQL EC2  │
                │ Ubuntu          │
                │ Docker          │
                │ PostgreSQL      │
                └─────────────────┘

## Technology Stack

### Cloud Platform
- AWS EC2
- AWS Security Groups
- Elastic IP

### Containerization
- Docker

### Backend Framework
- Django
- Python

### Database
- PostgreSQL

### Operating System
- Ubuntu Linux

### Version Control
- Git
- GitHub

---

## Project Features

- Dockerized Django Application
- Dockerized PostgreSQL Database
- Multi-EC2 Deployment Architecture
- Environment Variable-Based Configuration
- PostgreSQL Persistent Storage
- Database Migration Support
- Secure Network Communication
- Automatic Container Restart Policy
- Production-Oriented Architecture

---

## Infrastructure Details

| Component | Configuration |
|------------|--------------|
| Cloud Provider | AWS |
| Application Server | EC2 Instance |
| Database Server | EC2 Instance |
| Container Runtime | Docker |
| Backend Framework | Django |
| Database | PostgreSQL |
| OS | Ubuntu |
| Version Control | GitHub |

---

## Repository Structure

```text
aws-dockerized-django-postgresql-deployment/
│
├── app/
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── manage.py
│   ├── project/
│   └── .env.example
│
├── architecture/
│   └── architecture-diagram.png
│
├── screenshots/
│   ├── django-homepage.png
│   ├── admin-panel.png
│   ├── docker-containers.png
│   └── migrations-success.png
│
├── scripts/
│   ├── deploy.sh
│   ├── backup.sh
│   └── restore.sh
│
├── docs/
│   ├── installation-guide.md
│   └── troubleshooting.md
│
├── README.md
└── .gitignore
```

---

## AWS Security Group Configuration

### Application Server Security Group

| Port | Protocol | Purpose |
|--------|----------|----------|
| 22 | TCP | SSH Access |
| 8000 | TCP | Django Application |

### Database Server Security Group

| Port | Protocol | Purpose |
|--------|----------|----------|
| 22 | TCP | SSH Access |
| 5432 | TCP | PostgreSQL Access (Restricted) |

> PostgreSQL access is allowed only from the Django Application Server Security Group.

---

## Environment Variables

Create a `.env` file inside the Django project directory.

```env
DB_NAME=mydatabase
DB_USER=postgres
DB_PASSWORD=xx.xx
DB_HOST=172.31.x.x
DB_PORT=5432
SECRET_KEY=django-insecure-x8w3g5v9!@#7s2k...
DEBUG=False
```

---

## PostgreSQL Container Deployment

Pull PostgreSQL Image

```bash
docker pull postgres:16
```

Run PostgreSQL Container

```bash
docker run -d \
--name postgres-db \
--restart always \
-e POSTGRES_DB=mydatabase \
-e POSTGRES_USER=postgres \
-e POSTGRES_PASSWORD=xx.xx \
-v postgres_data:/var/lib/postgresql/data \
-p 5432:5432 \
postgres:16
```

Verify Container

```bash
docker ps
```

---

## Django Application Deployment

Build Docker Image

```bash
docker build -t django-app .
```

Run Django Container

```bash
docker run -d \
--name django-app \
--restart always \
-p 8000:8000 \
django-app
```

Verify Container

```bash
docker ps
```

---

## Database Migration

Run Migrations

```bash
docker exec -it django-app python manage.py migrate
```

Create Superuser

```bash
docker exec -it django-app python manage.py createsuperuser
```

Collect Static Files

```bash
docker exec -it django-app python manage.py collectstatic --noinput
```

---

## Validation Steps

### Verify Django Application

```bash
http://13.233.xxx.xxx:8000
```

### Verify Django Admin

```bash
http://13.233.xxx.xxx:8000/admin
```

### Verify Database Connectivity

```bash
docker exec -it django-app python manage.py dbshell
```

---

## Screenshots

Add screenshots for:

- EC2 Instances
- Docker Containers Running
- Django Home Page
- Django Admin Panel
- PostgreSQL Container
- Migration Success
- Security Group Configuration

---

## Challenges Faced

- Configuring Django to communicate with a remote PostgreSQL container.
- Managing AWS Security Group rules.
- Handling PostgreSQL persistent storage using Docker volumes.
- Troubleshooting database connectivity between EC2 instances.
- Managing environment variables securely.

---

## Learning Outcomes

Through this project, I gained practical experience in:

- AWS Infrastructure Management
- Docker Containerization
- Django Deployment
- PostgreSQL Administration
- Linux Server Management
- Networking and Security
- DevOps Best Practices
- Troubleshooting Production Deployments

---

## Future Enhancements

- Nginx Reverse Proxy
- HTTPS SSL Certificates
- Jenkins CI/CD Pipeline
- Terraform Infrastructure as Code
- Kubernetes Deployment
- Prometheus Monitoring
- Grafana Dashboards
- AWS Application Load Balancer
- Auto Scaling Implementation

---
