# ⚡ Terraform Provisioners

> **Provisioners are used to execute scripts or commands on a local machine or a remote resource after Terraform creates or destroys infrastructure.**
>
> Although Provisioners can automate post-deployment tasks, HashiCorp recommends using them only as a last resort because they are less predictable than declarative resource management.

---

# 📖 Table of Contents

* What are Provisioners?
* Why Do We Need Provisioners?
* Provisioner Workflow
* Types of Provisioners
* local-exec
* remote-exec
* file Provisioner
* Connection Block
* Provisioners on Destroy
* Best Practices
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What are Provisioners?

Provisioners execute scripts or commands after Terraform creates or destroys a resource.

They are mainly used for:

* Running shell commands
* Installing software
* Copying files
* Initial server configuration
* Running custom scripts

Provisioners work **after** Terraform creates the infrastructure.

---

# 🎯 Why Do We Need Provisioners?

Suppose Terraform creates an EC2 instance.

Without Provisioners:

```text id="b4r7t1"
Create EC2

↓

Login using SSH

↓

Install Nginx

↓

Configure Server

↓

Start Service
```

With Provisioners:

```text id="w8m2k5"
Create EC2

↓

Run Script Automatically

↓

Server Ready
```

This reduces manual work.

---

# 🔄 Provisioner Workflow

```text id="g5x8n3"
Terraform Configuration

↓

terraform apply

↓

Create Resource

↓

Run Provisioner

↓

Infrastructure Ready
```

Provisioners execute only after successful resource creation.

---

# ⚙️ Types of Provisioners

Terraform provides three commonly used Provisioners.

| Provisioner | Purpose                                                    |
| ----------- | ---------------------------------------------------------- |
| local-exec  | Executes commands on the machine running Terraform         |
| remote-exec | Executes commands on the remote resource                   |
| file        | Copies files from the local machine to the remote resource |

---

# 💻 local-exec Provisioner

Runs commands on the **local machine** where Terraform is executed.

Example:

```hcl id="d7p4v9"
resource "aws_instance" "web" {

  ami           = "ami-xxxxxxxx"

  instance_type = "t2.micro"

  provisioner "local-exec" {

    command = "echo EC2 Instance Created"

  }

}
```

Workflow:

```text id="n6q3m8"
Terraform

↓

EC2 Created

↓

Command Executes on Local Machine
```

Use Cases:

* Logging
* Sending notifications
* Running local scripts
* Updating inventory files

---

# 🌐 remote-exec Provisioner

Runs commands on the **remote resource**.

Example:

```hcl id="f8k2x6"
provisioner "remote-exec" {

  inline = [

    "sudo apt update",

    "sudo apt install -y nginx"

  ]

}
```

Workflow:

```text id="r4t9m1"
Terraform

↓

EC2 Created

↓

SSH Connection

↓

Commands Execute on EC2
```

Use Cases:

* Install packages
* Configure applications
* Start services
* Perform initial server setup

---

# 📂 file Provisioner

Copies files from the local machine to the remote resource.

Example:

```hcl id="m2v8q5"
provisioner "file" {

  source      = "index.html"

  destination = "/home/ubuntu/index.html"

}
```

Workflow:

```text id="k7x4p2"
Local Machine

↓

Copy File

↓

Remote Server
```

Use Cases:

* Configuration files
* Scripts
* Certificates
* Static website files

---

# 🔐 Connection Block

`remote-exec` and `file` require a connection block.

Example:

```hcl id="t9r3w7"
connection {

  type        = "ssh"

  host        = self.public_ip

  user        = "ubuntu"

  private_key = file("mykey.pem")

}
```

Common connection types:

* SSH (Linux)
* WinRM (Windows)

---

# 🗑️ Destroy Provisioner

Provisioners can also run **before a resource is destroyed**.

Example:

```hcl id="q5m7k4"
provisioner "local-exec" {

  when    = destroy

  command = "echo Resource Deleted"

}
```

Use Cases:

* Cleanup scripts
* Notifications
* Backup operations
* Logging

---

# ⚠️ Best Practices

HashiCorp recommends:

* Prefer cloud-init or user_data for instance configuration.
* Use configuration management tools such as Ansible, Chef, or Puppet for complex setup.
* Keep Provisioners simple and idempotent.
* Avoid using Provisioners for routine infrastructure management.
* Use them only when no better alternative exists.

---

# ☁️ DevOps Perspective

Typical production workflow:

```text id="j3v8r6"
Terraform

↓

Create EC2

↓

Cloud-Init / User Data

↓

(Optional)

Provisioner

↓

Application Ready
```

Modern DevOps pipelines often use **cloud-init**, **user_data**, or **configuration management tools** instead of heavy reliance on Provisioners.

---

# 🏭 Production Example

A company deploys a web server.

Terraform creates:

* EC2 Instance
* Security Group
* Elastic IP

After creation:

```text id="y6n2p8"
EC2 Created

↓

remote-exec

↓

Install Nginx

↓

Start Service

↓

Website Available
```

Another workflow:

```text id="v1k5t9"
Terraform

↓

local-exec

↓

Update Monitoring Inventory

↓

Deployment Notification
```

---

# 🎯 Common Interview Questions

### What are Terraform Provisioners?

Provisioners execute scripts or commands on local or remote machines after Terraform creates or destroys resources.

---

### What are the three main Provisioners?

* `local-exec`
* `remote-exec`
* `file`

---

### What is the difference between `local-exec` and `remote-exec`?

| local-exec                              | remote-exec                       |
| --------------------------------------- | --------------------------------- |
| Runs on the machine executing Terraform | Runs on the remote resource       |
| No SSH required                         | Requires a connection (SSH/WinRM) |

---

### Why does HashiCorp recommend avoiding Provisioners?

Because they are procedural, harder to maintain, and less predictable than Terraform's declarative model. Whenever possible, use cloud-init, `user_data`, or configuration management tools.

---

### When should Provisioners be used?

Only when no declarative Terraform resource or better automation mechanism can accomplish the task.

---

# 🔍 Useful Commands

Initialize project:

```bash id="e4r7m1"
terraform init
```

Preview execution:

```bash id="h8q2v5"
terraform plan
```

Apply infrastructure:

```bash id="n5x9k3"
terraform apply
```

Destroy infrastructure:

```bash id="p2t6w8"
terraform destroy
```

---

# 📑 Interview Cheat Sheet

```text id="c7m4r9"
Terraform

↓

Create Resource

↓

Provisioner

├── local-exec

├── remote-exec

└── file

↓

Configured Infrastructure
```

Remember:

* **Provisioners run after resource creation or before destruction**
* **`local-exec` executes on the local machine**
* **`remote-exec` executes on the remote resource**
* **`file` copies files to remote resources**
* **SSH or WinRM is required for remote execution**
* **Use Provisioners only as a last resort**
* **Prefer cloud-init, `user_data`, or Ansible for production configuration**

---

# 📚 Summary

Provisioners provide a way to execute scripts and perform post-deployment configuration tasks in Terraform. They support local command execution, remote command execution, and file transfers, making them useful for bootstrapping resources.

However, because Provisioners introduce procedural behavior into Terraform's declarative workflow, they should be used sparingly. In production environments, cloud-init, `user_data`, or dedicated configuration management tools are generally preferred for configuring infrastructure after provisioning.

---

# 🔗 Related Topics

⬅️ **Previous:** Lifecycle → `../12-Lifecycle/README.md`

➡️ **Next:** Best Practices → `../14-Best-Practices/README.md`

### 📖 Recommended Reading

* Terraform Best Practices
* Terraform Lifecycle
* Terraform Modules
* Cloud-Init Documentation
* Ansible Documentation
* Terraform Official Documentation
