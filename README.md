# Note API – CI/CD with GitHub Actions & Google Cloud Run

## Overview

This project demonstrates a **production-ready CI/CD pipeline** for a FastAPI-based Note API application. It emphasizes:

- Automated testing and coverage reporting
- Security scanning with Snyk
- Containerization with Docker
- Deployment to **Google Cloud Run**
- Observability with **OpenTelemetry**  

The pipeline ensures **fast feedback** on pull requests, continuous quality checks, and reliable deployment to a serverless environment.

---

## Features

### CI (Continuous Integration)

- Runs on **pull requests to `main`**
- Executes **unit tests** with **pytest**
- Measures **test coverage** using **pytest-cov**
- Uploads coverage reports to **Codecov**
- Performs **security scanning** with **Snyk**  

### CD (Continuous Deployment)

- Triggered after **CI pipeline completes successfully**
- Builds Docker image tagged with commit SHA
- Pushes image to **GitHub Container Registry (GHCR)**
- Copies image to **Google Artifact Registry**
- Deploys to **Google Cloud Run**
- Sets environment variables, including OpenTelemetry for tracing  

### Observability

- Traces all incoming requests using **OpenTelemetry**
- Sends traces to **Google Cloud Trace**
- Supports **custom spans** for monitoring specific API functions

---

## Architecture

```text
GitHub Repository
       │
       ├─ CI Pipeline (PR/Push)
       │    ├─ Checkout code
       │    ├─ Setup Python
       │    ├─ Install dependencies
       │    ├─ Run tests (pytest + coverage)
       │    └─ Security scan (Snyk)
       │
       └─ CD Pipeline (workflow_run)
            ├─ Checkout code
            ├─ Build & push Docker image to GHCR
            ├─ Authenticate with Google Cloud
            ├─ Push image to Google Artifact Registry
            └─ Deploy to Cloud Run (with OTEL)

