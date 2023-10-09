# Jenkins-ECR-Docker-Email-Integration
A DevOps project integrating Jenkins, AWS ECR, Docker for deployments, with email notifications for status updates, providing seamless automation and collaboration
## DevOps Pipeline with Email Notifications for AWS-Jenkins-ECR-Docker Deployment

This project showcases the implementation of a robust DevOps pipeline that automates the deployment of a Dockerized application using Jenkins, Amazon Web Services (AWS), and Amazon Elastic Container Registry (ECR). In addition to seamless deployment, it integrates email notifications to keep the stakeholders informed about the build and deployment status.

## Overview

**Jenkins-ECR-Docker-Email-Integration** is a comprehensive DevOps project designed to streamline your software development, testing, deployment, and notification processes. This project combines the power of Jenkins, AWS Elastic Container Registry (ECR), Docker, and email notifications to create a seamless and automated workflow.

## Project Highlights

- **Continuous Integration and Deployment (CI/CD):** Utilize Jenkins for continuous integration and deployment of your codebase.

- **Docker Containerization:** Build and manage Docker containers to ensure consistency across different environments.

- **Amazon ECR Integration:** Seamlessly push Docker images to Amazon Elastic Container Registry for reliable container storage and distribution.

- **Email Notifications:** Receive email notifications for build and deployment status updates, keeping your team informed at every stage.

- **Security:** Implement security groups to control access to instances, ensuring a secure deployment environment.

- **Easy Configuration:** Configure your project with clear and concise steps, making it accessible for both beginners and experienced DevOps practitioners.

- **Domain Integration:** Register your domain with AWS and set up an Application Load Balancer (ALB) to provide a user-friendly web interface for your application.

## Email Notifications

One of the key highlights of this project is its integration with email notifications. Email notifications serve as a crucial communication channel to inform team members and stakeholders about the status of the deployment pipeline. Here's how it works:

- **Send Email Notification Stage:** This project includes a dedicated stage in the Jenkins pipeline responsible for sending email notifications. Upon successful completion of the deployment pipeline, an email notification is triggered automatically.
  ![image](https://github.com/HarshGupta-coder/Jenkins-ECR-Docker-Email-Integration/assets/54001485/4a0abc5d-62c3-4b42-aad9-45898d16676b)


### Notification Content

The email notification includes the following information:

- **Subject:** Build Status - Indicates whether the build and deployment were successful.
- **Body:** Provides a direct link to access the deployed application and additional information about the build.
- **Recipient:** The email is sent to the specified recipient(s) to keep them updated.

## Project Setup

### Table of Contents

1. [Security Groups](#step-1-security-groups)
2. [Launch Main Instance](#step-2-launch-main-instance)
3. [Launch Deploy Instance](#step-3-launch-deploy-instance)
4. [Create IAM User](#step-4-create-iam-user)
5. [Create ECR Repository](#step-5-create-ecr-repository)
6. [SSH Setup](#step-6-ssh-setup)
7. [Jenkins Configuration](#step-7-jenkins-configuration)
8. [Jenkins Credentials](#step-8-jenkins-credentials)
9. [SSH Key in Jenkins](#step-9-ssh-key-in-jenkins)
10. [Email Notifications](#step-10-email-notifications)
11. [Jenkins Pipeline](#step-11-jenkins-pipeline)
12. [Security Group Updates](#step-12-security-group-updates)
13. [Domain and ACM](#step-13-domain-and-acm)
14. [Elastic Load Balancer (ELB)](#step-14-elastic-load-balancer-elb)
15. [Test the Project](#step-15-test-the-project)
16. [Project Completion](#project-completion)

### Step 1: Security Groups

Create two security groups (SG):
- `main-sg`: For the main EC2 instance.
  - Allow HTTP traffic on port 8080 for Jenkins.
  - Allow SSH on port 22.
- `deploy-sg`: For the deploy EC2 instance.
  - Allow SSH traffic from `main-sg` and your IP address (for testing).

### Step 2: Launch Main Instance

Launch the main EC2 instance with a UserData script provided in the repo. Attach `main-sg` to the main EC2 instance.

### Step 3: Launch Deploy Instance

Launch the deploy EC2 instance with a UserData script provided in the repo. Attach `deploy-sg` to the deploy EC2 instance.

### Step 4: Create IAM User

Create an IAM user with necessary permissions for your pipeline and download the access keys.

### Step 5: Create ECR Repository

Create an ECR repository named `task-1`.

### Step 6: SSH Setup

SSH into both instances. On the main instance, generate an SSH key pair, and on the deploy instance, add the public key to the `authorized_keys` file.

### Step 7: Jenkins Configuration

Access the main instance at `public-ip:8080` and configure Jenkins.

### Step 8: Jenkins Credentials

In Jenkins, add AWS Access Key and AWS Secret Key with IDs `aws-access-key` and `aws-secret-key` as secret text.

### Step 9: SSH Key in Jenkins

Add the private key from the main instance to Jenkins credentials with ID `ssh-credentials` as SSH Username with a private key.

### Step 10: Email Notifications

In Jenkins, configure email notifications in "Manage Jenkins" > "Configure System."

### Step 11: Jenkins Pipeline

Create a Jenkins pipeline script according to the repo and adjust your settings.

### Step 12: Security Group Updates

Configure `deploy-sg` to allow traffic from the ELB on ports 80 and 443.

### Step 13: Domain and ACM

Set up an ACM certificate for your domain and configure your domain's DNS settings to point to the ELB.

### Step 14: Elastic Load Balancer (ELB)

Create an Application Load Balancer (ALB) with the desired settings, including listeners, security groups, and actions.

### Step 15: Test the Project

Access your domain URL and verify the project's functionality.

### Project Completion

Congratulations! You have successfully set up a DevOps pipeline and deployed your project.


## Usage

This section provides guidance on how to use the DevOps pipeline and deploy your project.

### 1. Triggering the Pipeline

- Push code changes to your GitHub repository. This will trigger the Jenkins pipeline automatically if you've configured GitHub Webhooks.

### 2. Jenkins Pipeline

- The Jenkins pipeline script defined in the project's repo automates the following stages:
  - Code checkout from your GitHub repository.
  - Building a Docker image with a unique tag.
  - Pushing the Docker image to Amazon Elastic Container Registry (ECR).
  - Deploying the Docker image to your EC2 instances.
  - Sending email notifications on build completion.

- To customize the pipeline:
  - Adjust environment variables in the pipeline script for your AWS settings.
  - Modify the Docker image build process as needed.
  - Extend or customize deployment steps based on your project requirements.

### 3. Monitoring and Notifications

- Jenkins will monitor your GitHub repository for code changes and trigger the pipeline accordingly.
- You will receive email notifications on the success or failure of each build.

### 4. Accessing Your Deployed Application

- Once the pipeline is successfully completed, access your deployed application:
  - Use the URL of your Elastic Load Balancer (ELB) or your custom domain (after DNS propagation).
  - Verify that your application is running as expected.

### 5. Maintenance and Scaling

- As your project evolves, you can make changes to the pipeline script, update your application code, and scale your infrastructure as needed.

### 6. Troubleshooting

- If any issues arise during deployment or notifications, refer to the Jenkins console output and logs for detailed information.
- Check AWS services (ECR, EC2, ELB) for any errors or issues.

Please follow these steps to effectively use and manage your DevOps pipeline. For further assistance, refer to the project documentation or consult AWS and Jenkins documentation for troubleshooting and advanced configurations.


## Usage

This section provides guidance on how to use the DevOps pipeline and deploy your project.

### 1. Triggering the Pipeline

- Push code changes to your GitHub repository. This will trigger the Jenkins pipeline automatically if you've configured GitHub Webhooks.

### 2. Jenkins Pipeline

- The Jenkins pipeline script defined in the project's repo automates the following stages:
  - Code checkout from your GitHub repository.
  - Building a Docker image with a unique tag.
  - Pushing the Docker image to Amazon Elastic Container Registry (ECR).
  - Deploying the Docker image to your EC2 instances.
  - Sending email notifications on build completion.

- To customize the pipeline:
  - Adjust environment variables in the pipeline script for your AWS settings.
  - Modify the Docker image build process as needed.
  - Extend or customize deployment steps based on your project requirements.

### 3. Monitoring and Notifications

- Jenkins will monitor your GitHub repository for code changes and trigger the pipeline accordingly.
- You will receive email notifications on the success or failure of each build.

### 4. Accessing Your Deployed Application

- Once the pipeline is successfully completed, access your deployed application:
  - Use the URL of your Elastic Load Balancer (ELB) or your custom domain (after DNS propagation).
  - Verify that your application is running as expected.

### 5. Maintenance and Scaling

- As your project evolves, you can make changes to the pipeline script, update your application code, and scale your infrastructure as needed.

### 6. Troubleshooting

- If any issues arise during deployment or notifications, refer to the Jenkins console output and logs for detailed information.
- Check AWS services (ECR, EC2, ELB) for any errors or issues.

Please follow these steps to effectively use and manage your DevOps pipeline. For further assistance, refer to the project documentation or consult AWS and Jenkins documentation for troubleshooting and advanced configurations.


