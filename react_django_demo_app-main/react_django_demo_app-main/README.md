# React-Django Web App on AWS ECR and ECS

This guide will walk you through the process of deploying a full-stack web application using React for the front end and Django for the back end on AWS Elastic Container Registry (ECR) and Elastic Container Service (ECS). You will also set up an EC2 instance for managing the deployment.

## Prerequisites

Before you begin, ensure you have the following prerequisites:

- An AWS account
- An EC2 instance (AMI: Ubuntu)
- SSH access to the EC2 instance
- Docker and AWS CLI installed on your EC2 instance
- AWS credentials configured on the EC2 instance using `aws configure`
- A public GitHub repository for your web app (e.g., [https://github.com/yourusername/your-repo](https://github.com/yourusername/your-repo))

## Setup

### 1. EC2 Instance

- Create an EC2 instance named 'ECR_ECS' with the Ubuntu AMI.
- Allow inbound traffic on port 8000 in the security group.

### 2. SSH into the EC2 Instance

SSH into the EC2 instance and clone your web app repository from GitHub:

```bash
ssh -i your-key.pem ubuntu@your-instance-public-ip
git clone https://github.com/yourusername/your-repo.git
3. Install Docker and AWS CLI
Install Docker and AWS CLI on the EC2 instance:

bash
Copy code
# Install Docker
sudo apt-get update
sudo apt-get install docker.io

# Install AWS CLI
sudo apt-get install awscli
4. Configure AWS CLI
Run aws configure and enter the AWS access key and secret key for your AWS account.

5. Create a Public ECR Repository
Create an ECR repository for your web app on the AWS Console.
Take note of the repository URI.
6. Build and Push Docker Images
On the EC2 instance, navigate to your cloned repository:

bash
Copy code
cd your-repo

# Build and push the Docker images to the ECR repository
docker build -t your-repo-frontend .
docker tag your-repo-frontend:latest your-ecr-repo-uri/your-repo-frontend:latest
docker push your-ecr-repo-uri/your-repo-frontend

docker build -t your-repo-backend .
docker tag your-repo-backend:latest your-ecr-repo-uri/your-repo-backend:latest
docker push your-ecr-repo-uri/your-repo-backend
7. Create an ECS Cluster
Create an ECS cluster from the AWS Console.

8. Configure Task Definitions
In the ECS Console, select 'Task Definitions'.
Create a new task definition, specifying the task name and container name.
Use the ECR image URIs for your frontend and backend containers.
Click 'Create'.
9. Run Your Task
Choose your ECS cluster and click 'Run Task'.
Create a new security group allowing traffic on port 8000.
Click 'Run Task'.
10. Access Your Application
Copy the public IP of the ECS container with port 8000, and your site will be live.
