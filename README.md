# BSCS-2212333 — DevOps Final Project

**Student Name:** Muhammad Abbas Hassan
**Registration Number:** BSCS-2212333
**Course:** DevOps Fundamentals
**Live Application URL:** http://16.171.152.63:8000

---

# Project Overview

This project demonstrates a complete DevOps workflow using Docker, Docker Compose, GitHub Actions, PostgreSQL, and AWS EC2.

The application is a containerized FastAPI microservice connected to a PostgreSQL database. Continuous Integration (CI) automatically runs linting and tests on every push and pull request, while Continuous Deployment (CD) automatically deploys the latest version to an AWS EC2 instance whenever code is pushed to the main branch.

---

# Application Architecture

```text
GitHub Repository
       │
       ▼
GitHub Actions CI
 ├── flake8 Linting
 └── pytest Testing
       │
       ▼
GitHub Actions CD
       │
       ▼
SSH into AWS EC2
       │
       ▼
Docker Compose Deployment
       │
 ┌─────┴─────┐
 ▼           ▼
FastAPI    PostgreSQL
(Web)      (Database)
```

## Components

| Component        | Technology            | Description                    |
| ---------------- | --------------------- | ------------------------------ |
| Web Service      | FastAPI + Uvicorn     | REST API running on port 8000  |
| Database         | PostgreSQL 15         | Persistent relational database |
| Containerization | Docker                | Application packaging          |
| Orchestration    | Docker Compose        | Multi-container deployment     |
| CI Pipeline      | GitHub Actions        | flake8 + pytest                |
| CD Pipeline      | GitHub Actions + SSH  | Automatic deployment to EC2    |
| Cloud Platform   | AWS EC2 Ubuntu Server | Production hosting environment |

---

# API Endpoints

## GET /health

Returns application health and database status.

### Example Response

```json
{
  "status": "ok",
  "db": "connected",
  "student": "BSCS-2022-001"
}
```

---

## POST /students

Creates a new student record.

### Example Request

```json
{
  "reg_no": "BSCS-2212333",
  "name": "Muhammad Abbas Hassan",
  "semester": 8,
  "section": "B"
}
```

---

## GET /students

Returns all stored student records.

---

## GET /students/{reg_no}

Returns a specific student record by registration number.

---

# Local Development Setup

## Prerequisites

* Docker
* Docker Compose
* Python 3.12

## Clone Repository

```bash
git clone https://github.com/MAbbasHassan/BSCS-2212333-devops-project.git
cd BSCS-2212333-devops-project
```

## Configure Environment Variables

```bash
cp .env.example .env
```

Edit the `.env` file according to your local environment.

## Start Services

```bash
docker compose up --build
```

## Verify Application

```bash
curl http://localhost:8000/health
curl http://localhost:8000/students
```

---

# Running Tests

Install dependencies:

```bash
pip install -r requirements.txt
```

Run tests:

```bash
pytest app/tests/ -v
```

Run linting:

```bash
flake8 app/ --max-line-length=100
```

---

# Production Deployment (AWS EC2)

## Connect to EC2

```bash
ssh -i devops-project.pem ubuntu@16.171.152.63
```

## Deploy Application

```bash
cd ~/devops-project
git pull origin main
cp .env.production .env
docker compose -f docker-compose.prod.yml up -d --build
```

---

# GitHub Actions Workflows

## Continuous Integration (CI)

Automatically runs:

* flake8 linting
* pytest test suite

Triggered on:

* Push
* Pull Request

## Continuous Deployment (CD)

Automatically:

* SSHs into EC2
* Pulls latest code
* Rebuilds Docker containers
* Restarts application

Triggered on:

* Push to main branch

---

# GitHub Secrets Used

| Secret      | Purpose         |
| ----------- | --------------- |
| EC2_HOST    | EC2 Public IP   |
| EC2_USER    | Ubuntu User     |
| EC2_SSH_KEY | EC2 Private Key |

---

# Project Structure

```text
BSCS-2212333-devops-project
│
├── app
│   ├── main.py
│   ├── database.py
│   ├── models.py
│   └── tests
│       ├── conftest.py
│       ├── test_health.py
│       └── test_students.py
│
├── Dockerfile
├── docker-compose.yml
├── docker-compose.prod.yml
├── requirements.txt
├── .env.example
├── .gitignore
├── .dockerignore
│
├── .github
│   └── workflows
│       ├── ci.yml
│       └── cd.yml
│
└── README.md
```

---

# Live Deployment

Application URL:

```text
http://16.171.152.63:8000
```

Swagger Documentation:

```text
http://16.171.152.63:8000/docs
```

---

# Author

**Muhammad Abbas Hassan**
**BSCS-2212333**
DevOps Fundamentals Final Project


*DevOps Fundamentals — Instructor: Afaq Ahmed*
