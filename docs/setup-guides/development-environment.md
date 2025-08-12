# DevOps Development Environment Setup Guide

This guide helps you set up a comprehensive DevOps development environment for all portfolio projects. Follow the sections relevant to your current phase of development.

## Phase 1: Basic GitHub & Documentation Setup

### Prerequisites
- GitHub account
- Git installed locally
- Text editor (VS Code recommended)
- Web browser

### GitHub Repository Setup

#### 1. Create Central Portfolio Repository
```bash
# Create repository on GitHub.com first, then clone locally
git clone https://github.com/yourusername/devops-portfolio-overview.git
cd devops-portfolio-overview

# Create initial structure
mkdir -p docs/{setup-guides,architecture}
mkdir -p templates resources

# Add README and initial files
# (Copy content from artifacts provided)
```

#### 2. Repository Organization Best Practices
```bash
# Pin important repositories to profile
# Go to GitHub Profile → Repositories → Click "Pin" on:
# - devops-portfolio-overview
# - observability-stack
# - terraform-multi-environment
# - kubernetes-gitops-pipeline

# Set up branch protection rules for main repositories
# Repository Settings → Branches → Add rule for main branch
```

#### 3. Professional GitHub Profile Optimization
```markdown
# Add to your GitHub profile README (username/username repository):
## DevOps Engineer | Infrastructure Automation | Cloud Architecture

🔧 Building scalable infrastructure with Terraform, Kubernetes, and AWS
📊 Implementing comprehensive monitoring solutions with Prometheus & Grafana
🚀 Creating efficient CI/CD pipelines and GitOps workflows

📍 Currently working on: [Link to devops-portfolio-overview]
```

## Phase 2: Local Development Environment

> **⚠️ Switch to Linux Environment Recommended**
> 
> For Phase 2 and beyond, working on a Linux machine will provide the best experience for DevOps tools and workflows.

### Core DevOps Tools Installation

#### 1. Docker & Container Tools
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install docker.io docker-compose
sudo usermod -aG docker $USER
# Log out and back in for group changes to take effect

# Verify installation
docker --version
docker-compose --version
```

#### 2. Kubernetes Tools
```bash
# Install kubectl
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

# Install kind (Kubernetes in Docker) for local development
go install sigs.k8s.io/kind@v0.20.0
# OR download binary from: https://kind.sigs.k8s.io/docs/user/quick-start/

# Install Helm
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```

#### 3. Terraform & Infrastructure Tools
```bash
# Install Terraform
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform

# Install Terragrunt (optional, for advanced Terraform workflows)
wget https://github.com/gruntwork-io/terragrunt/releases/download/v0.50.0/terragrunt_linux_amd64
sudo mv terragrunt_linux_amd64 /usr/local/bin/terragrunt
sudo chmod +x /usr/local/bin/terragrunt

# Verify installation
terraform --version
```

#### 4. AWS CLI & Cloud Tools
```bash
# Install AWS CLI v2
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

# Configure AWS CLI (you'll need AWS account)
aws configure
# Enter: Access Key ID, Secret Access Key, Default region, Output format

# Verify installation
aws --version
aws sts get-caller-identity
```

### Development Tools Setup

#### 1. VS Code with DevOps Extensions
```bash
# Install VS Code
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/trusted.gpg.d/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt update
sudo apt install code

# Essential extensions (install through VS Code):
# - HashiCorp Terraform
# - Kubernetes
# - Docker
# - YAML
# - GitLens
# - Remote Development
```

#### 2. Monitoring Stack Prerequisites
```bash
# Ensure Docker Compose is ready for monitoring stack
docker-compose --version

# Create directory for monitoring projects
mkdir -p ~/devops-projects/observability-stack
cd ~/devops-projects/observability-stack

# This is where you'll migrate your existing Prometheus/Grafana setup
```

### Project-Specific Setup

#### 1. Terraform Project Structure
```bash
mkdir -p ~/devops-projects/terraform-multi-environment/{environments/{dev,staging,prod},modules,global}
cd ~/devops-projects/terraform-multi-environment

# Initialize Terraform project structure
terraform init
```

#### 2. Kubernetes Development Environment
```bash
# Create local Kubernetes cluster with kind
kind create cluster --name devops-portfolio

# Verify cluster
kubectl cluster-info --context kind-devops-portfolio
kubectl get nodes
```

## Environment Variables & Configuration

### 1. Shell Configuration
```bash
# Add to ~/.bashrc or ~/.zshrc
export PATH=$PATH:/usr/local/bin
export KUBECONFIG=~/.kube/config

# AWS CLI completion
complete -C '/usr/local/bin/aws_completer' aws

# Terraform completion
complete -C /usr/bin/terraform terraform

# Reload shell configuration
source ~/.bashrc
```

### 2. Git Configuration for Professional Commits
```bash
# Set up professional Git identity
git config --global user.name "Your Full Name"
git config --global user.email "your.professional@email.com"
git config --global init.defaultBranch main

# Set up SSH key for GitHub (recommended)
ssh-keygen -t ed25519 -C "your.professional@email.com"
# Add public key to GitHub: Settings → SSH and GPG keys
```

## Verification & Testing

### 1. Tool Verification Script
```bash
#!/bin/bash
# Save as verify-setup.sh and run to check all tools

echo "=== DevOps Environment Verification ==="
echo "Docker: $(docker --version)"
echo "Docker Compose: $(docker-compose --version)"
echo "Kubernetes: $(kubectl version --client)"
echo "Helm: $(helm version)"
echo "Terraform: $(terraform --version)"
echo "AWS CLI: $(aws --version)"
echo "Git: $(git --version)"
echo "=== Verification Complete ==="
```

### 2. Quick Test Deployments
```bash
# Test Docker
docker run hello-world

# Test Kubernetes cluster
kubectl run test-pod --image=nginx --port=80
kubectl get pods

# Test Terraform
terraform version

# Clean up test resources
kubectl delete pod test-pod
```

## File Migration Strategy

### From Work Computer
When you're ready to migrate files from your work computer:

```bash
# 1. Archive your monitoring stack
tar -czf monitoring-stack-backup.tar.gz /path/to/monitoring/files

# 2. Transfer via secure method:
# - Cloud storage (Google Drive, AWS S3)
# - Git repository (if appropriate)
# - External drive

# 3. Extract and organize in new environment
cd ~/devops-projects/observability-stack
tar -xzf monitoring-stack-backup.tar.gz
```

## Next Steps Checklist

### Phase 1 (Current)
- [ ] Create devops-portfolio-overview repository
- [ ] Set up professional GitHub profile
- [ ] Create all planned repository structures
- [ ] Import calendar deadlines

### Phase 2 (Linux Environment)
- [ ] Complete local development environment setup
- [ ] Migrate existing monitoring stack
- [ ] Begin Terraform multi-environment project
- [ ] Set up local Kubernetes development cluster

### Ongoing Maintenance
- [ ] Weekly tool updates: `sudo apt update && sudo apt upgrade`
- [ ] Docker image cleanup: `docker system prune`
- [ ] Git repository maintenance: `git gc --aggressive`

---

**Need Help?**
- Documentation issues: Create issue in devops-portfolio-overview repository
- Tool-specific problems: Check official documentation links below
- Environment questions: Review this guide and update as needed

**Reference Links:**
- [Docker Documentation](https://docs.docker.com/)
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Terraform Documentation](https://www.terraform.io/docs)
- [AWS CLI Documentation](https://docs.aws.amazon.com/cli/)

*Last Updated: August 10, 2025*
