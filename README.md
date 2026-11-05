# 🚀 Node.js CI/CD Pipeline Automation Using GitHub Actions

## 📌 Project Overview

This project demonstrates how to automate the build, test, and deployment process of a Node.js web application using a CI/CD pipeline.

I created this project as part of my **DevOps Internship at Elevate Labs**.

The pipeline uses GitHub Actions to automatically test the application, build a Docker image, push the image to Docker Hub, and deploy the application on an AWS EC2 instance.

## 🎯 Project Objectives

- Automate application testing.
- Build Docker images automatically.
- Push Docker images to Docker Hub.
- Deploy applications on AWS EC2.
- Understand the complete CI/CD process.
- Reduce manual deployment work.

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Git | Version control |
| GitHub | Source code repository |
| GitHub Actions | CI/CD automation |
| Node.js | Application runtime |
| Docker | Containerization |
| Docker Hub | Docker image registry |
| AWS EC2 | Application hosting |
| Ubuntu Linux | Server operating system |

## 🏗️ Project Architecture

The CI/CD pipeline follows this process:

1. Developer writes application code.
2. Developer pushes code to GitHub.
3. GitHub Actions automatically triggers the workflow.
4. Node.js application dependencies are installed.
5. Application tests are executed.
6. Docker image is built.
7. Docker image is pushed to Docker Hub.
8. GitHub Actions connects to AWS EC2 through SSH.
9. EC2 pulls the Docker image and runs the container.
10. Application becomes accessible through the EC2 public IP.

## 📂 Project Structure

```text
nodejs-demo-app/
│
├── .github/
│   └── workflows/
│       └── main.yml
│
├── app.js
├── package.json
├── package-lock.json
├── Dockerfile
└── README.md
```

## ⚙️ Application Details

The application is developed using Node.js.

It runs on port 3000 and displays the following message:

**Hello! DevOps CI/CD Pipeline is Working!**

### package.json

The package.json file contains application information and scripts.

```json
{
  "name": "nodejs-demo-app",
  "version": "1.0.0",
  "description": "DevOps CI/CD Demo Application",
  "main": "app.js",
  "scripts": {
    "start": "node app.js",
    "test": "node --check app.js"
  }
}
```

## 🐳 Docker Configuration

The Dockerfile is used to create a Docker image of the Node.js application.

```dockerfile
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./

RUN npm ci

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

### Dockerfile Explanation

- FROM: Selects the Node.js base image.
- WORKDIR: Creates the working directory.
- COPY: Copies application files.
- RUN: Installs dependencies.
- EXPOSE: Declares application port 3000.
- CMD: Starts the Node.js application.

## 🔄 CI/CD Pipeline Using GitHub Actions

The workflow file is located at:

`.github/workflows/main.yml`

The pipeline contains three jobs:

### 1. Test Application

- Checks out the source code.
- Sets up Node.js.
- Installs dependencies.
- Runs the application syntax test.

### 2. Build and Push Docker Image

- Configures Docker Buildx.
- Logs in to Docker Hub.
- Builds the Docker image.
- Pushes the image to Docker Hub.

### 3. Deploy on AWS EC2

- Connects to the EC2 instance using SSH.
- Pulls the Docker image.
- Stops the previous container.
- Removes the previous container.
- Runs the new application container.

The `needs` keyword ensures that jobs execute in the correct order.

## 🔐 GitHub Secrets Configuration

Sensitive information is stored securely using GitHub Repository Secrets.

The following secrets are configured:

| Secret Name | Description |
|---|---|
| DOCKERHUB_USERNAME | Docker Hub username |
| DOCKERHUB_TOKEN | Docker Hub access token |
| EC2_HOST | EC2 public IP address |
| EC2_USER | EC2 Linux username |
| EC2_SSH_KEY | EC2 private SSH key |

**Security:** Credentials and private keys are not stored directly in the workflow file.

## ☁️ AWS EC2 Deployment

AWS EC2 is used to host the Node.js application.

Deployment steps:

1. Launch an Ubuntu EC2 instance.
2. Configure SSH and HTTP security group rules.
3. Install Docker.
4. Configure GitHub Secrets.
5. Connect to EC2 using SSH.
6. Pull the Docker image.
7. Run the Docker container.
8. Access the application through the EC2 public IP.

Application URL:

```text
http://YOUR_EC2_PUBLIC_IP
```

The EC2 Linux username must match the actual account configured on the server. For a standard Ubuntu EC2 image, it is usually `ubuntu`.

## 🧪 Testing the Application Locally

Install dependencies:

```bash
npm install
```

Check JavaScript syntax:

```bash
npm test
```

Run the application:

```bash
npm start
```

Build the Docker image:

```bash
docker build -t nodejs-demo-app .
```

Run the Docker container:

```bash
docker run -d -p 3000:3000 nodejs-demo-app
```

Open:

```text
http://localhost:3000
```

## 🛠️ Errors Faced During Project Implementation

During this project, I faced several practical errors while configuring Node.js, Git, GitHub, and GitHub Actions.

### 1. npm Command Not Recognized

**Error:**

```text
npm is not recognized as an internal
or external command
```

**Reason:** Node.js was not installed or was not added to the Windows PATH.

**Solution:** Installed Node.js LTS and restarted VS Code.

### 2. PowerShell Execution Policy Error

**Error:**

```text
npm.ps1 cannot be loaded because
running scripts is disabled
```

**Reason:** PowerShell execution policy blocked the npm PowerShell script.

**Solution:**

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

Alternatively, used Command Prompt to execute npm commands.

### 3. Git Commit Error

**Error:**

```text
pathspec did not match any file(s) known to git
```

**Reason:** The Git commit command was written incorrectly.

**Solution:**

```bash
git add .
git commit -m "Initial CI/CD project"
```

### 4. Git Push Error

**Error:**

```text
src refspec main does not match any
```

**Reason:** There was no initial commit available to push.

**Solution:** Created the initial commit and pushed the main branch.

### 5. Git Remote Already Exists

**Error:**

```text
remote origin already exists
```

**Reason:** The origin remote had already been configured.

**Solution:** Verified the existing remote using:

```bash
git remote -v
```

### 6. GitHub Internal Server Error

**Error:**

```text
remote: Internal Server Error
```

**Reason:** GitHub temporarily rejected the push due to a server-side error.

**Solution:** Retried the Git push after checking the repository connection.

### 7. GitHub Actions Workflow Not Showing

**Problem:** The GitHub Actions page displayed "Get started with GitHub Actions" instead of the pipeline.

**Reason:** The workflow file was initially placed inside the `.github` folder instead of the required `workflows` subfolder.

**Incorrect location:**

```text
.github/main.yml
```

**Correct location:**

```text
.github/workflows/main.yml
```

**Solution:**

```bash
mkdir -p .github/workflows

git mv .github/main.yml .github/workflows/main.yml

git commit -m "Fix workflow location"

git push origin main
```

This helped GitHub identify the workflow file.

## 🎓 Interview Questions and Answers

### 1. What is CI/CD?

CI/CD stands for Continuous Integration and Continuous Delivery or Continuous Deployment.

It automates building, testing, and deploying applications.

### 2. What is GitHub Actions?

GitHub Actions is a CI/CD automation tool provided by GitHub. It automatically runs workflows when events such as code pushes occur.

### 3. What is a workflow?

A workflow is an automated process defined in a YAML file. It contains jobs and steps that execute specific tasks.

### 4. What are runners?

Runners are machines that execute GitHub Actions workflows.

For example, `ubuntu-latest` is a GitHub-hosted runner.

### 5. What is the difference between jobs and steps?

- Job: A group of tasks executed on a runner.
- Step: An individual task inside a job.

### 6. How do you secure secrets in GitHub Actions?

I use GitHub Repository Secrets to store sensitive information such as Docker Hub tokens, passwords, and SSH private keys.

### 7. How do you handle deployment errors?

I check GitHub Actions logs, identify the failed job or step, troubleshoot the issue, fix it, and rerun the workflow.

### 8. Explain the Docker build and push workflow.

First, Docker builds an image using the Dockerfile. Then GitHub Actions logs in to Docker Hub and pushes the image to the Docker registry.

### 9. How can you test a CI/CD pipeline locally?

I test the application using npm commands and build and run the Docker container locally.

### 10. What is Docker?

Docker is a containerization platform that packages applications and their dependencies into containers.

### 11. What is a Docker image?

A Docker image is a read-only template used to create Docker containers.

### 12. What is a Docker container?

A Docker container is a running instance of a Docker image.

### 13. What is Docker Hub?

Docker Hub is a cloud-based registry used to store and share Docker images.

### 14. What is AWS EC2?

Amazon EC2 is a cloud computing service that provides virtual servers to run applications.

### 15. Why did you use GitHub Secrets?

I used GitHub Secrets to protect sensitive credentials and prevent them from being exposed in the source code.

### 16. What is SSH?

SSH stands for Secure Shell. It is used to securely connect to remote servers.

### 17. What is the purpose of the needs keyword?

The `needs` keyword defines job dependencies. It ensures that one job runs only after its required previous job succeeds.

### 18. What triggers your pipeline?

My pipeline is triggered automatically whenever code is pushed to the `main` branch. It can also be started manually using workflow dispatch.

### 19. What is the difference between Continuous Delivery and Continuous Deployment?

Continuous Delivery prepares and validates code for release, often with manual production approval.

Continuous Deployment automatically releases successfully validated changes to production.

### 20. What did you learn from this project?

I learned how to automate application testing, Docker image building, image pushing, and deployment using GitHub Actions and AWS EC2. I also learned practical troubleshooting of Git, Node.js, Docker, and CI/CD errors.

## 📈 Key Learnings

- Understanding CI/CD pipeline automation.
- Working with Git and GitHub.
- Creating GitHub Actions workflows.
- Writing Dockerfiles.
- Building and pushing Docker images.
- Configuring GitHub Secrets.
- Deploying applications on AWS EC2.
- Troubleshooting real-world DevOps errors.

## 👨‍💻 Author

**Aman Maniyar**

BCA Graduate | AWS Cloud & DevOps

GitHub: https://github.com/maniyaraman744-hue

Project Repository: https://github.com/maniyaraman744-hue/nodejs-demo-app

---

**Conclusion**

This project helped me understand the practical implementation of a CI/CD pipeline using GitHub Actions, Docker, Docker Hub, and AWS EC2. It provided hands-on experience with automation, containerization, cloud deployment, and troubleshooting.
