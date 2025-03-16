# Jenkins Pipeline for vProfile Project

## Overview

This Jenkins pipeline automates the build, test, and deployment process for the **vProfile** project. It includes code fetching, building, testing, static code analysis, Docker image creation, and deployment to AWS ECS.

## Prerequisites

Before running this pipeline, ensure you have the following:

- **Jenkins** installed and configured
- **Maven 3.9** installed and available as `MAVEN3.9`
- **JDK 17** installed and available as `JDK17`
- **SonarQube** configured as `sonarserver`
- **AWS credentials** stored in Jenkins as `awscreds`
- **Docker installed** on the Jenkins agent
- **AWS CLI installed and configured** for ECS deployment

## Pipeline Stages

### 1. **Fetch Code**

- Clones the `docker` branch of the vProfile project repository from GitHub.

### 2. **Build**

- Runs `mvn install -DskipTests` to compile the project and package it into a `.war` file.
- Archives the build artifact for later use.

### 3. **Unit Tests**

- Executes `mvn test` to run unit tests.

### 4. **Checkstyle Analysis**

- Runs `mvn checkstyle:checkstyle` to check for code style violations.

### 5. **SonarQube Code Analysis**

- Uses SonarQube scanner to analyze code quality and generate reports.

### 6. **Quality Gate**

- Waits for SonarQube's quality gate results and fails the pipeline if the code does not meet quality standards.

### 7. **Build App Image**

- Uses Docker to build a container image from the application code.
- The image is built using the multi-stage Dockerfile located in `./Docker-files/app/multistage/`.

### 8. **Upload App Image**

- Pushes the Docker image to the specified container registry.
- Tags the image with the Jenkins build number and `latest`.

### 9. **Remove Container Images**

- Removes all local Docker images to free up space.

### 10. **Deploy to AWS ECS**

- Updates the ECS service to deploy the new application version.
- Forces a new deployment to ensure the latest Docker image is used.

## How to Use

1. Ensure that all prerequisites are met.
2. Configure necessary credentials and environment variables in Jenkins.
3. Trigger the pipeline manually or via a webhook when new code is pushed to the repository.
4. Monitor pipeline execution via Jenkins logs and dashboards.
5. Verify deployment on AWS ECS.

## Troubleshooting

- **Pipeline fails at SonarQube Analysis**: Ensure that SonarQube is running and `sonarserver` is correctly configured in Jenkins.
- **Docker build issues**: Verify that Docker is installed and the `appRegistry` variable is correctly set.
- **AWS Deployment fails**: Check AWS CLI permissions and ECS cluster/service names.

## Conclusion

This Jenkins pipeline automates the CI/CD process for the vProfile project, ensuring efficient and reliable deployments to AWS ECS.
