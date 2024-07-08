# CI/CD with Jenkins

## Overview
This repository demonstrates a complete CI/CD pipeline using Jenkins. It showcases how to build, test, and deploy a Java application while integrating static code analysis, Docker containerization, and deployment to Kubernetes.

## Features
- **Automated Build**: Builds the Java project using Maven.
- **Static Code Analysis**: Utilizes SonarQube to perform code quality checks.
- **Unit Testing**: Executes tests and reports results using Maven.
- **Dockerization**: Builds and pushes Docker images to a registry.
- **Kubernetes Deployment**: Deploys the application to a Kubernetes cluster.

## Prerequisites
- Java 8 or higher
- Maven
- Docker
- Kubernetes (e.g., Minikube, EKS, GKE)
- Jenkins with necessary plugins installed:
  - Pipeline
  - Git
  - Maven Integration
  - SonarQube Scanner
  - Docker Pipeline

## Setup Instructions

### Clone the Repository
```bash
git clone https://github.com/davraops/ci-cd-with-jenkins.git
cd ci-cd-with-jenkins

# Configure Jenkins

## Set up Jenkins Credentials

1. **Navigate to "Manage Jenkins" > "Manage Credentials".**
2. **Store credentials for SonarQube and Docker registry:**
   - **SonarQube Credentials**: Add a 'Username with password' credential for SonarQube access.
   - **Docker Registry Credentials**: Add a 'Username with password' credential for Docker registry access.

## Install Necessary Plugins

- Ensure your Jenkins setup has all required plugins installed and configured.

## Configure Environment Variables

Set up environment variables in your Jenkins pipeline configuration for:
- `SONARQUBE_SERVER`: URL to your SonarQube server.
- `REGISTRY_URL`: URL to your Docker registry.
- `DOCKER_IMAGE`: Name of the Docker Image to be used.
- `REGISTRY_CREDENTIALS`: The Jenkins credentials ID for your Docker registry
- `REGISTRY_URL`: The URL to your Docker registry (e.g., docker.io or myregistry.com)

# CI/CD Pipeline

## Pipeline Stages

1. **Checkout**: Clones the code from GitHub.
2. **Build**: Compiles the project using Maven.
3. **Static Code Analysis**: Runs SonarQube analysis using credentials securely.
4. **Test**: Runs unit tests with Maven.
5. **Build Docker Image**: Builds a Docker image of the application.
6. **Push Docker Image**: Pushes the image to a Docker registry using secured credentials.
7. **Deploy**: Deploys the application to a Kubernetes cluster.

## Jenkinsfile

- Refer to the `Jenkinsfile` in the repository which contains the detailed pipeline configuration. It utilizes environment variables and credentials stored in Jenkins to manage sensitive data securely.

# Usage

## Running the Pipeline

1. **Start a Build**: Trigger a build from the Jenkins dashboard.
2. **Monitor Output**: View the pipeline execution in real time within Jenkins to verify each step.

# Contributing

- Contributions are welcome. Please fork the repository and submit a pull request with your changes.
