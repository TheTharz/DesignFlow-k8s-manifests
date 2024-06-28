# CI/CD Pipeline for MERN Stack Application

## Overview

This project demonstrates a CI/CD pipeline for deploying a MERN (MongoDB, Express.js, React, Node.js) stack application using various DevOps tools and practices. The pipeline is designed to ensure code quality, security, and automated deployments.

## Diagrams

### Figure 1.1 - CI/CD Pipeline Workflow
![CICD3 drawio](https://github.com/TheTharz/DesignFlow-k8s-manifests/assets/119271523/c0bacd7f-0bc9-468a-b47e-0aedec513cba)

### Figure 1.2 - CI Pipeline Workflow
![Untitled Diagram drawio (4)](https://github.com/TheTharz/DesignFlow-k8s-manifests/assets/119271523/cc2f7485-cca8-4af4-a718-ffc19ad55158)

### Figure 1.3 - CD Pipeline Workflow
![Untitled Diagram drawio (5)](https://github.com/TheTharz/DesignFlow-k8s-manifests/assets/119271523/ba833eff-b3ac-4307-a29a-c2fe924efa75)

## Components and Their Roles

### GitHub
- **Role:** Source code repository.
- **Functionality:** Central source of codebase where developers push code changes.

### Jenkins
- **Role:** Continuous Integration tool.
- **Functionality:** Orchestrates the CI/CD pipeline, including building the application, running tests, performing static code analysis with SonarQube, scanning images with Trivy, and deploying to Docker Hub.

### SonarQube
- **Role:** Code quality and security analysis tool.
- **Functionality:** Integrates with Jenkins to perform static code analysis, ensuring the code adheres to quality and security standards before deployment.

### Trivy
- **Role:** Vulnerability scanning tool.
- **Functionality:** Used in Jenkins to scan Docker images for vulnerabilities before they are pushed to Docker Hub.

### Docker
- **Role:** Containerization platform.
- **Functionality:** Jenkins uses Docker to build application images, which are then stored in Docker Hub and deployed to Kubernetes.

### Docker Hub
- **Role:** Container registry.
- **Functionality:** Stores Docker images built by Jenkins. These images are tagged with the build number and are accessible for deployment to the Kubernetes cluster.

### Ansible
- **Role:** Configuration management tool.
- **Functionality:** Deploys the application using Ansible playbooks, configuring the environment and preparing it for deployment. Ansible scripts manage the deployment process to the Kubernetes cluster.

### Kubernetes
- **Role:** Container orchestration tool.
- **Functionality:** Manages the deployment, scaling, and operation of Docker containers within a Kubernetes cluster.

### Application Containers
- **Role:** Runtime environment for the application.
- **Functionality:** The MERN stack application is deployed in multiple Docker containers within the Kubernetes cluster.

### Terraform
- **Role:** Infrastructure as Code (IaC) tool.
- **Functionality:** Manages the provisioning and configuration of cloud infrastructure. Terraform scripts are used to set up the necessary resources on AWS.

### Argo CD
- **Role:** Continuous Delivery and GitOps tool.
- **Functionality:** Automates the deployment of applications to Kubernetes clusters. Argo CD continuously monitors a GitOps repository where the desired state of the application (defined using Kubernetes manifests) is stored. It ensures that the actual state of the Kubernetes cluster matches the desired state by automatically synchronizing the changes from the GitOps repository.

## Connectivity

### Code Commit and Trigger
- Developer pushes code to GitHub.
- GitHub webhook triggers a Jenkins pipeline.

### Build and Test
- Jenkins pulls the code from GitHub.
- Jenkins runs unit tests and static code analysis using SonarQube.
- Jenkins builds a Docker image.
- Jenkins scans the Docker image using Trivy.

### Push to Docker Hub
- Jenkins pushes the built Docker image to Docker Hub.

### Infrastructure Provisioning
- Terraform sets up the necessary EC2 instances, VPCs, and other resources.
- Ansible may be used to configure these instances if needed.

### Continuous Delivery with Argo CD
- The desired state of the application (Kubernetes manifests) is stored in a GitOps repo.
- Argo CD continuously monitors this GitOps repo.
- Argo CD deploys the application to the Kubernetes cluster running on EC2 instances.
- Argo CD ensures the cluster state matches the desired state in the GitOps repo.

### Monitoring and Notifications
- Jenkins sends build and deployment notifications to Slack and email.
- Any failures or alerts are communicated immediately for rapid response.

## Automation Approach

### DevOps Tools
- **GitHub:** v2.33
- **Jenkins:** v2.319.3
- **Ansible:** v2.9
- **Kubernetes:** v1.30.0
- **Node:** v19.*.*
- **SonarQube:** v8.9.0
- **Trivy**
- **Docker:** v23.0.0
- **Argo CD:** v2.11.3
- **Terraform:** v1.9.0

### Other Tools and Dependencies
- **Ubuntu:** v22.0.4
- **EC2 Instances:** t2.medium instances

### Application Tools and Dependencies
- **MongoDB:** v8.0
- **Express.js:** v4.19.1
- **React:** v18.0.0
- **Node.js:** v19.0.0

## Automated Deployment Process

In this DevOps pipeline for deploying a MERN stack application, GitHub serves as the central source code repository where developers push their code changes. When code is pushed, a GitHub webhook triggers Jenkins, a Continuous Integration (CI) tool that orchestrates the CI/CD pipeline. Jenkins pulls the code from GitHub, runs unit tests, performs static code analysis using SonarQube to ensure code quality, and builds Docker images of the application. These images are scanned for vulnerabilities using Trivy before being pushed to Docker Hub, a container registry. For deployment, Terraform provisions the necessary infrastructure on AWS EC2, setting up VPCs and instances, while Ansible is used for configuration management and deployment to Kubernetes. The desired state of the application, defined in a GitOps repository, is continuously monitored and deployed by Argo CD to ensure the Kubernetes cluster matches this state. Application containers are managed within the Kubernetes cluster, ensuring scalability and reliability. Throughout the process, Jenkins sends notifications to Slack and email to keep the team informed of build and deployment statuses, promptly alerting them to any issues. This integrated approach ensures a streamlined and secure deployment pipeline from code commit to application deployment.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any improvements or suggestions.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
