# ⚙️ Terraform Installation

> **Before using Terraform to provision infrastructure, it must be installed and configured on your local machine or server.**
>
> This guide explains how to install Terraform, verify the installation, configure your environment, and understand the basic project structure.

---

# 📖 Table of Contents

* Why Install Terraform?
* System Requirements
* Installation Methods
* Installing on Linux (Ubuntu)
* Installing on Windows
* Installing on macOS
* Verify Installation
* Terraform Project Structure
* First Terraform Project
* DevOps Perspective
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ Why Install Terraform?

Terraform is a command-line tool that communicates with cloud providers to provision infrastructure.

Before creating resources, Terraform must be installed and initialized.

After installation, you can:

* Create Infrastructure
* Update Resources
* Destroy Infrastructure
* Manage Cloud Environments
* Automate Infrastructure Deployment

---

# 💻 System Requirements

Terraform supports:

* Linux
* Windows
* macOS

Supported Architectures:

* x86_64
* ARM64

Internet access is required during initialization to download Terraform Providers.

---

# 🚀 Installation Methods

Terraform can be installed using:

* Package Manager
* Official Binary
* ZIP Package
* Homebrew (macOS)
* Chocolatey (Windows)

The recommended approach is using the official HashiCorp repository or binary.

---

# 🐧 Installing on Ubuntu

### Step 1: Update Packages

```bash id="h2v4gf"
sudo apt update
```

---

### Step 2: Install Required Packages

```bash id="ws1jz2"
sudo apt install -y wget gpg software-properties-common
```

---

### Step 3: Add the HashiCorp GPG Key

```bash id="y6k8ed"
wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null
```

---

### Step 4: Add the HashiCorp Repository

```bash id="9eh9zk"
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list
```

---

### Step 5: Update Repository

```bash id="9xh4wd"
sudo apt update
```

---

### Step 6: Install Terraform

```bash id="jlwm6w"
sudo apt install terraform
```

---

# 🪟 Installing on Windows

1. Download Terraform from the HashiCorp website.
2. Extract the ZIP file.
3. Add the Terraform executable to the **PATH** environment variable.
4. Open PowerShell or Command Prompt.
5. Verify the installation.

---

# 🍎 Installing on macOS

Using Homebrew:

```bash id="aw5ynr"
brew tap hashicorp/tap

brew install hashicorp/tap/terraform
```

---

# ✅ Verify Installation

Check the installed version:

```bash id="0egifg"
terraform version
```

Example Output:

```text id="j08lnd"
Terraform v1.x.x
```

Display all available commands:

```bash id="1dnhuo"
terraform
```

View help:

```bash id="njlwmu"
terraform --help
```

---

# 📂 Terraform Project Structure

A basic Terraform project looks like:

```text id="nfd6bl"
terraform-project/

├── main.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
└── providers.tf
```

Purpose of each file:

| File               | Purpose                        |
| ------------------ | ------------------------------ |
| `main.tf`          | Main infrastructure resources  |
| `providers.tf`     | Cloud provider configuration   |
| `variables.tf`     | Input variables                |
| `terraform.tfvars` | Variable values                |
| `outputs.tf`       | Output values after deployment |

---

# 🚀 Creating Your First Project

Create a project directory:

```bash id="bglfwl"
mkdir terraform-demo

cd terraform-demo
```

Create configuration files:

```bash id="55qjj6"
touch main.tf

touch providers.tf

touch variables.tf

touch outputs.tf

touch terraform.tfvars
```

Your project is now ready for writing Terraform configurations.

---

# ☁️ DevOps Perspective

A typical Terraform workflow begins after installation.

```text id="r7v4xq"
Install Terraform

↓

Create Project

↓

Write Configuration

↓

terraform init

↓

terraform plan

↓

terraform apply
```

This workflow is commonly integrated into CI/CD pipelines for automated infrastructure deployment.

---

# 🏭 Production Example

A DevOps Engineer needs to provision AWS infrastructure.

Workflow:

```text id="fqtjlj"
Install Terraform

↓

Clone Infrastructure Repository

↓

terraform init

↓

terraform plan

↓

terraform apply

↓

AWS Infrastructure Created
```

Every team member uses the same Terraform version and configuration, ensuring consistent deployments.

---

# 🎯 Common Interview Questions

### How do you verify Terraform installation?

```bash id="zpj8f4"
terraform version
```

---

### Which command displays Terraform help?

```bash id="oz8h6k"
terraform --help
```

---

### What is the purpose of `main.tf`?

It contains the primary infrastructure resources that Terraform manages.

---

### Which file stores variable definitions?

```text id="vc55ps"
variables.tf
```

---

### Which file stores output values?

```text id="gsyqtr"
outputs.tf
```

---

# 🔍 Useful Commands

```bash id="ewobpv"
terraform version

terraform --help

terraform fmt

terraform validate

terraform init

terraform plan

terraform apply

terraform destroy
```

---

# 📑 Interview Cheat Sheet

```text id="8mfpfm"
Install Terraform

↓

Verify Installation

↓

Create Project

↓

Write Configuration

↓

terraform init

↓

terraform plan

↓

terraform apply
```

Remember:

* **Install Terraform before creating infrastructure**
* **Verify installation using `terraform version`**
* **`main.tf` contains infrastructure resources**
* **`variables.tf` stores input variables**
* **`outputs.tf` displays output values**
* **Always run `terraform init` before using a new project**

---

# 📚 Summary

Installing Terraform is the first step toward Infrastructure as Code. Once installed, Terraform enables developers and DevOps engineers to define, provision, and manage cloud infrastructure using code instead of manual configuration.

A properly configured Terraform environment provides a consistent foundation for infrastructure automation, version control, and scalable cloud deployments.

---

# 🔗 Related Topics

⬅️ **Previous:** Introduction → `../01-Introduction/README.md`

➡️ **Next:** Terraform Architecture → `../03-Terraform-Architecture/README.md`

### 📖 Recommended Reading

* Terraform Architecture
* Providers
* Resources
* HashiCorp Configuration Language (HCL)
* Terraform Official Documentation
