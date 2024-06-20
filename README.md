# Automated EKS Cluster Creation Using Jenkins & Terraform
To automate the creation of an EKS cluster using Jenkins and Terraform, set up your infrastructure as code (IaC) and CI/CD pipeline. This involves creating Terraform scripts to define EKS cluster and configuring Jenkins to execute these scripts automatically.

# Prerequisites
  1. AWS Account
  2. Local Machine Requirements
       Operating System: Linux, macOS, or Windows
       Command Line Tools
       Terminal (Linux/macOS) or Git Bash (Windows).
  3. Installed Software
        Terraform: Infrastructure as code tool.
        AWS CLI: Command-line interface for AWS.
        kubectl: Kubernetes command-line tool.
  4. Jenkins: Automation server - An EC2 instance - server running Jenkins.
  5. Version Control System 
     GitHub Account: To Store Terraform scripts and Jenkinsfile.

# Step 1
Installer file is to automate the installations required for creating High-availability Infrastructure. 
 >>> This script installs the Java, Jenkins, Terraform and Kubernetes Installations
# Step 2
Create a Directory for Terraform Scripts 
# Step 3
- Configure Jenkins Pipeline
- Add a Jenkinsfile to Your GitHub Repository
# Step 4
- Create kubernetes/deployment.yaml
- Create kubernetes/service.yaml
# Step 5 Launch EC2 instance
 
>>>Launch an Instance
>>>Choose an Ubuntu
>>>Choose an Instance Type (t3.micro)
>>>Configure Instance Details
   -Accept the default settings for most options.
   -Under "Network", ensure you have a VPC selected.
   -Click "Next: Add Storage".
>>>Add Storage
    -Add any tags to your instance (e.g., Key: Name, Value: MyInstance) to help identify it.
    -Click "Next: Configure Security Group".
    -Configure Security Group:
>>>Create a new security group or select an existing one.
     -Add rules to allow SSH access (port 22) from your IP address.
     -Add rules to allow TCP access (port 80) from your IP address - For Jenkins
     -If you plan to host a web server, also add rules for HTTP (port 80) and HTTPS (port 443).
     -Click "Review and Launch".
>>>Advance Settings - User data to Add the shell script for installations -- This installs the Java, Jenkins, Terraform and Kubernetes on the server.
>>>Review Instance Launch
     -Review your settings and click "Launch".
     -Select an Existing Key Pair or Create a New Key Pair
     -Create a new one and download it. This key pair will be used to SSH into your instance.
     -If you already have a key pair, you can use that.
     -Acknowledge that you have access to the key pair and click "Launch Instances".
>>>View Instances:
     -Click "View Instances" to see your newly launched instance.
     -Wait for the instance to enter the "running" state.
>>>Create IAM Role for EC2 Instance

# Step 6 Configure Jenkins for CI/CD

>>>Access Jenkins:
   -Open your browser and navigate to http://<your-ec2-public-ip>:8080.
>>>Install Necessary Plugins
>>>Create Jenkins Credentials
   AWS Credentials: Add AWS access key and secret key as Jenkins credentials.
   Kubeconfig: Add the kubeconfig file for your EKS cluster as a Jenkins credential.
   GitHub: Repository link
>>>Create a Jenkins Pipeline Job
    -Create a Pipeline Job
    -Go to Jenkins Dashboard.
    -Click on "New Item".
    -Enter a name for your job and select "Pipeline".
    -In Jenkins, create a new Pipeline job and configure it to use the following 'Jenkinsfile' from GitHub repository.
>>>Configure the Jenkins Pipeline
   - In the Pipeline section of the Jenkins job configuration, set the Pipeline script to use the Jenkinsfile from repository.
     
# Step 7 Trigger the Jenkins Pipeline
  
   - We can manually trigger the pipeline job in Jenkins
   - This creates an eks cluster
>>>Verify Deployment
   - Interacting with EKS cluster
       aws eks update-kubeconfig --region us-east-1 --name eks-demo-cluster1 #update the kubeconfig
       kubectl run nginx --image=nginx  #to create nginx pod
    -Check Kubernetes Pods
     kubectl get pods
>>>Access the Application
     kubectl get svc 
