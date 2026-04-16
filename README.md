# CI/CD Pipeline with Jenkins, Maven, SonarQube, Docker, Kubernetes and Argo CD
[Screenshot 2023-03-28 at 9 38 09 PM](https://user-images.githubusercontent.com/43399466/228301952-abc02ca2-9942-4a67-8293-f76647b6f9d8.png)
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


## Project Structure

```
ci-cd-pipeline-project/
│
├── Dockerfile
├── Jenkinsfile
│
├── app/
│   ├── pom.xml
│   └── src/
│
├── k8s/
│   ├── deployment.yml
│   └── service.yml
│
├── argocd/
│   └── argocd-basic.yaml
│
├── docs/
└── README.md
```
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
docker build -t cicd-pipleine:v1 .

Run Docker Image
docker run -d -p 8010:8080 -t cicd-pipeline:v1

```

###  Final Project Image


<img width="1919" height="978" alt="image" src="https://github.com/user-attachments/assets/f2578db9-4497-44c3-90b9-f8006c9aa99a" />


## Requirments 


### Java code hosted on a repository
### Jenkins server
### Kubernetes cluster
### Helm package manager
### ArgoCD


### Launch a AWS Instance 

## Aim for 8 GB of memory





### Install Java and Jenkins

## Install Java 
```
sudo apt update
sudo apt install openjdk-17-jre
```

## Install Jenkins
``` curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

sudo chmod 644 /usr/share/keyrings/jenkins-keyring.asc

echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install -y fontconfig openjdk-17-jre jenkins
```

Open Port 8080 In the Traffic Inbound Rules on AWS as by defeault AWS has restricted jenkins accessibility by deafault 

Configure Jenkins 

## Login into Jenkins



Run the command to gain access to the password - sudo cat /var/lib/jenkins/secrets/initialAdminPassword


After Select install Sugested Plugins and procede to login in to Jenkins



### Install Docker in Jenkins

Go to Manage Plugins and install Docker Pipeline


As We are using Docker Agents our Jenkins Pipelines as it makes the complexity of our configuration easier rather than having to install different dependencies on each ec2 everytime we scale up


## Install Docker

```
sudo apt update
sudo apt install docker.io
```

### Configure SonarQube



SonarQube may seem complicated to install however if you follow all these steps i have simplified it down for you and you should have no problem downloading it.

Make sure you are logged into your ubuntu@Ipadress 
```sudo Su - ```

Now you Should be in your Root@Ipaddress

```
adduser sonarqube
Sudo install unzip
```

Now Switch to your sonarqube

```
sudo su sonarqube
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-10.4.1.88267.zip
unzip *
exit
sudo mv /home/sonarqube/sonarqube-10.4.1.88267 /opt/sonarqube
sudo chown -R sonarqube:sonarqube /opt/sonarqube
cd /opt/sonarqube/bin/linux-x86-64
./sonar.sh status
```


Check if its running

```
./sonar.sh status
```

Open on http://<your-ec2-ip>:9000

Username : admin
Password : admin



Create a Token on sonar qube 




Link it to your Jenkins 

Go to Manage Jenkins then Security then Credentials 

Fill in your secret choose a name and leave the description Blank



### Docker Configuration

## Install Docker

``` Sudo apt install docker.io```

### Grant Jenkins and Ubuntu Permission to access docker and then restart
```sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
```
 


### Kubernetes Configuration

Follow the Doccumentation on the Officall Kubernetes Website to Download and after downloaded Follow along

MINIKUBE IS REQUIRED



