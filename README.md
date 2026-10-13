# 🛒 ShopEasy — AWS EC2 One-Click Deployment Using Jenkins CI/CD

ShopEasy is a sample e-commerce frontend project used to learn and implement end-to-end DevOps practices. The project focuses on automating the build and deployment process using GitHub, Jenkins, npm, AWS EC2, and Nginx.

The main goal is to simplify application deployment by creating a CI/CD workflow that takes source code from GitHub, builds the application, and deploys the generated files to an AWS EC2 instance where Nginx serves the application to users.

## 📌 Project Overview

- **Project Name:** ShopEasy
- **Project Type:** E-commerce frontend deployment
- **Cloud Platform:** Amazon Web Services (AWS)
- **Compute Service:** Amazon EC2
- **Version Control:** Git
- **Source Code Management:** GitHub
- **CI/CD Tool:** Jenkins
- **Build Tool:** npm
- **Web Server:** Nginx
- **Operating System:** Linux (Ubuntu, if used on EC2)
- **Access:** Web browser through the EC2 public IP or configured domain

## 🎯 Project Objective

The objective of this project is to understand how a frontend application can be built and deployed automatically using DevOps tools.

The project demonstrates how to:

- Maintain application source code in GitHub.
- Automate build and deployment tasks using Jenkins.
- Install dependencies and build the application using npm.
- Deploy application files to an AWS EC2 instance.
- Configure Nginx to serve the deployed frontend.
- Access the deployed application through a web browser.
- Understand the end-to-end CI/CD workflow.

## 🏗️ Project Architecture

```text
             Developer
                 |
                 v
          Git / GitHub
                 |
                 v
           Jenkins CI/CD
                 |
                 v
       Clone Source Code
                 |
                 v
       Install Dependencies
             npm install
                 |
                 v
          Build Application
            npm run build
                 |
                 v
       Deploy Build Artifacts
                 |
                 v
             AWS EC2
                 |
                 v
            Nginx Server
                 |
                 v
          ShopEasy Frontend
                 |
                 v
             Web Browser
```

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Git | Version control |
| GitHub | Source code hosting |
| Jenkins | CI/CD automation |
| Node.js | JavaScript runtime required by the build environment |
| npm | Dependency management and build commands |
| AWS EC2 | Cloud server for hosting the application |
| Linux | Server administration |
| Nginx | Web server for serving frontend files |
| HTML, CSS, JavaScript | Frontend technologies, depending on the application |

## 🔄 CI/CD Workflow

### 1. Source Code Management

The ShopEasy source code is maintained in a GitHub repository. Git is used to track changes and manage the source code.

### 2. Jenkins Pipeline

Jenkins is used to automate the application build and deployment workflow. It checks out the source code and executes the configured pipeline steps.

### 3. Dependency Installation

The required application dependencies are installed using npm.

```bash
npm install
```

### 4. Application Build

The application is built using the build script defined in `package.json`.

```bash
npm run build
```

The generated output directory depends on the frontend framework and project configuration.

### 5. Deployment to AWS EC2

The generated build files are transferred to the EC2 instance using the deployment method configured in Jenkins, such as SSH and file transfer.

### 6. Nginx Configuration

Nginx serves the deployed frontend files over HTTP or HTTPS, depending on the server configuration.

### 7. Application Access

Users access the deployed application through a browser using the EC2 public IP address or a configured domain name.

## ⚙️ Prerequisites

Before setting up the project, ensure you have:

- An AWS account.
- A running EC2 instance.
- A GitHub account and ShopEasy repository.
- Jenkins installed and running.
- Git installed in the Jenkins build environment.
- Node.js and npm installed in the build environment.
- SSH access to the EC2 instance.
- Nginx installed on the EC2 instance.
- Appropriate EC2 security group rules.
- The required Jenkins credentials for deployment.

## 🚀 Installation and Setup

### Step 1: Clone the Repository

Clone the ShopEasy repository to your local machine or Jenkins build environment.

```bash
git clone https://github.com/Swaroop-93/ShopEasy.git
cd ShopEasy
```

Replace the repository URL and directory name with the actual values for your project.

### Step 2: Install Dependencies

Install the application dependencies.

```bash
npm install
```

### Step 3: Build the Application

Run the configured frontend build command.

```bash
npm run build
```

Confirm that the build completes successfully and identify the output directory, such as `dist/` or `build/`, according to your framework.

### Step 4: Launch an AWS EC2 Instance

1. Sign in to the AWS Management Console.
2. Open the EC2 service.
3. Launch an instance using a suitable Linux distribution.
4. Configure the required security group rules.
5. Connect to the instance using SSH.

Allow inbound HTTP traffic on port 80 if you intend to serve the application over HTTP. Restrict SSH access to trusted IP addresses.

### Step 5: Install Nginx on Ubuntu

Connect to the EC2 instance and execute:

```bash
sudo apt update
sudo apt install nginx -y
```

Enable and start Nginx:

```bash
sudo systemctl enable nginx
sudo systemctl start nginx
```

Check the service status:

```bash
sudo systemctl status nginx
```

### Step 6: Configure Jenkins

Create a Jenkins job or pipeline for the ShopEasy repository.

The pipeline should perform the following tasks:

1. Retrieve the source code from GitHub.
2. Install application dependencies.
3. Build the application.
4. Transfer the generated build files to the EC2 instance.
5. Deploy the files to the configured Nginx document root.
6. Report whether the pipeline succeeded or failed.

Configure the required repository and SSH credentials securely through Jenkins.

### Step 7: Deploy the Build Files

Deploy the contents of the actual build output directory to the Nginx document root configured on your EC2 instance.

For example, Ubuntu's default Nginx document root is commonly `/var/www/html`. Confirm the active Nginx configuration before deploying.

A manual deployment example, when the build output is `dist/`, is:

```bash
sudo cp -r dist/. /var/www/html/
```

Run this command on the server only after the build files have been transferred to the server and the target directory has been verified.

The final deployment should use the same destination configured in your Jenkins pipeline.

### Step 8: Access the Application

Open a browser and navigate to:

```text
http://<EC2_PUBLIC_IP>
```

Replace `<EC2_PUBLIC_IP>` with your instance's actual public IPv4 address.

If DNS and HTTPS have been configured, use your domain name instead.

## 📂 Repository Structure

The following is an illustrative structure for a frontend application. The actual files and directories depend on your repository.

```text
ShopEasy/
├── public/
├── src/
├── package.json
├── package-lock.json
├── Jenkinsfile
└── README.md
```

### File and Directory Description

- `public/` — Public static assets, if used.
- `src/` — Frontend application source code, if used by the framework.
- `package.json` — Project metadata, dependencies, and npm scripts.
- `package-lock.json` — Locked npm dependency versions.
- `Jenkinsfile` — Jenkins pipeline definition, if pipeline-as-code is used.
- `README.md` — Project documentation and setup instructions.

## 🔐 Security Best Practices

- Never commit AWS credentials, passwords, private SSH keys, or tokens to GitHub.
- Store sensitive deployment credentials in Jenkins Credentials.
- Restrict SSH access to trusted IP addresses.
- Allow only necessary inbound network traffic in the EC2 security group.
- Use HTTPS for production deployments.
- Verify build artifacts before replacing deployed files.
- Keep the operating system, Jenkins, and application dependencies updated.
- Implement a backup and rollback strategy for important deployments.

## 🧪 Testing and Troubleshooting

### Check Nginx Status

```bash
sudo systemctl status nginx
```

### Validate Nginx Configuration

```bash
sudo nginx -t
```

### Restart Nginx

```bash
sudo systemctl restart nginx
```

### Check Nginx Error Logs

```bash
sudo tail -n 100 /var/log/nginx/error.log
```

### Common Issues

**Application does not load**

- Verify the EC2 public IP address.
- Confirm that inbound HTTP traffic is allowed on port 80.
- Check the Nginx service status.
- Verify that the deployed files exist in the configured document root.

**Jenkins build fails**

- Review the Jenkins console output.
- Confirm that Git, Node.js, and npm are installed in the appropriate environment.
- Verify the repository URL and configured credentials.
- Confirm that the npm build script exists and completes successfully.

**Deployment fails**

- Check SSH connectivity between Jenkins and EC2.
- Verify deployment credentials and remote directory permissions.
- Confirm that the source build directory and destination directory are correct.

## 📈 Future Enhancements

The following are potential extensions to the project, not confirmed components of the original deployment workflow.

- **Docker:** Containerize the application.
- **Docker Hub:** Store and distribute container images.
- **Kubernetes:** Orchestrate container deployments.
- **Prometheus:** Collect application and infrastructure metrics.
- **Grafana:** Create monitoring dashboards.
- **SonarQube:** Analyze code quality.
- **Trivy:** Scan container images and dependencies for vulnerabilities.
- **Terraform:** Provision AWS infrastructure as code.
- **Argo CD:** Automate Kubernetes deployments using GitOps.
- **HTTPS:** Configure secure application access with TLS.
- **Notifications:** Add Jenkins build and deployment notifications.

## 📚 Key Learning Outcomes

Through this project, the following DevOps concepts can be practiced:

- Version control with Git and GitHub.
- CI/CD automation using Jenkins.
- Frontend dependency management and build processes using npm.
- AWS EC2 provisioning and server administration.
- Linux command-line operations.
- Nginx installation and configuration.
- Application deployment and troubleshooting.
- SSH-based server access and deployment security.
- Understanding the complete flow from source code to a running web application.

## 👨‍💻 Author

**Makina Jyothi Swaroop**

Cloud & DevOps Engineering Enthusiast

- GitHub: https://github.com/Swaroop-93
- LinkedIn: https://www.linkedin.com/in/jyothi-swaroop-makina-3a158a35b

This project was created to gain practical experience with AWS, Jenkins, CI/CD automation, Linux, and Nginx-based web application deployment.

## 📄 License

Add the license applicable to this repository before distributing the project. If you choose the MIT License, include a `LICENSE` file containing the appropriate license text.

---

⭐ If you find this project useful, feel free to explore the repository and build upon the deployment workflow.
