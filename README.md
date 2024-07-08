# CIC with Jenkins

## Overview
This repository demonstrates a complete CI/CD pipeline using Jenkins. The pipeline includes build, test, static code analysis, Docker containerization, and deployment to a Kubernetes cluster.

## Features
- **Automated Build**: Using Maven to build the project.
- **Static Code Analysis**: Integrated with SonarQube for code quality checks.
- **Unit Testing**: Runs tests and reports results.
- **Dockerization**: Builds and pushes Docker images.
- **Kubernetes Deployment**: Deploys the application to a Kubernetes cluster.

## Prerequisites
- Java 8 or higher
- Maven
- Docker
- Kubernetes (Minikube or a remote cluster)
- Jenkins
- SonarQube

## Setup Instructions

### Clone the Repository
```bash
git clone https://github.com/davraops/ci-cd-with-jenkins.git
cd ci-cd-with-jenkins
