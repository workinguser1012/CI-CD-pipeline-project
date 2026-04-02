# Jenkins Pipeline for Java based application using Maven, SonarQube, Argo CD, Helm and Kubernetes

![Screenshot 2023-03-28 at 9 38 09 PM](https://user-images.githubusercontent.com/43399466/228301952-abc02ca2-9942-4a67-8293-f76647b6f9d8.png)

# CI/CD Pipeline with Jenkins, Maven, SonarQube, Docker, Kubernetes and Argo CD

## Project Overview
This project demonstrates an end-to-end CI/CD pipeline for a Java Spring Boot application. It automates the process of building, testing, analyzing code quality, containerizing, and deploying the application to Kubernetes using a GitOps approach.

The pipeline integrates multiple DevOps tools to simulate a real-world software delivery workflow.

---

## Tech Stack
- Java (Spring Boot)
- Maven (Build tool)
- Jenkins (CI pipeline)
- SonarQube (Code quality analysis)
- Docker (Containerization)
- Kubernetes (Deployment)
- Argo CD (GitOps continuous delivery)

---

## Project Structure
.
├── Dockerfile
├── Jenkinsfile
├── app/
│ ├── pom.xml
│ └── src/
│
├── k8s/
│ ├── deployment.yml
│ └── service.yml
│
├── argocd/
│ └── argocd-basic.yaml
│
├── docs/
└── README.md

---

## CI/CD Pipeline Workflow

1. Code is pushed to the repository  
2. Jenkins pipeline is triggered  
3. Application is built using Maven (`mvn clean package`)  
4. Unit tests are executed  
5. SonarQube performs code quality analysis  
6. Application is packaged into a JAR file  
7. Docker image is built  
8. Image is pushed to a container registry  
9. Kubernetes manifests define deployment  
10. Argo CD syncs and deploys the application to the cluster  

---

## SonarQube Code Analysis

This pipeline integrates SonarQube to ensure high code quality and maintainability.

- Performs static code analysis during the CI stage  
- Detects bugs, vulnerabilities, and code smells  
- Enforces quality checks before deployment  

This ensures that only validated and maintainable code progresses through the pipeline.

---

## Key Components

### Jenkins Pipeline
- Automates the CI/CD workflow  
- Executes build, test, and analysis stages  
- Integrates with SonarQube and Docker  

### Maven Build
- Compiles Java application  
- Runs tests  
- Packages application into a JAR file  

### Docker
- Builds container image from application  
- Ensures consistent runtime environment  

### Kubernetes
- Manages application deployment and scaling  
- Uses YAML manifests for configuration  

### Argo CD
- Implements GitOps deployment strategy  
- Continuously syncs cluster state with Git repository  

---

## How to Run Locally

### Build the application
```bash
cd app
mvn clean package

Build Docker Image
docker build -t your-dockerhub-username/app-name .

Push Docker image
docker push your-dockerhub-username/app-name


Deploy to Kubernetes
kubectl apply -f k8s/

Apply Argo CD configuration
kubectl apply -f argocd/argocd-basic.yaml
