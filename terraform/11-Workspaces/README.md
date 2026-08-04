# 🏢 Terraform Workspaces

> **Terraform Workspaces allow you to manage multiple environments (such as Development, Testing, Staging, and Production) using the same Terraform configuration while maintaining separate State files.**
>
> Instead of duplicating Terraform code for each environment, Workspaces enable infrastructure isolation with minimal configuration changes.

---

# 📖 Table of Contents

* What are Workspaces?
* Why Do We Need Workspaces?
* Problems Without Workspaces
* Workspace Architecture
* Default Workspace
* Creating Workspaces
* Switching Workspaces
* Listing Workspaces
* Deleting Workspaces
* Workspace State Files
* Workspaces vs Separate Directories
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What are Workspaces?

A **Workspace** is an isolated environment that maintains its own Terraform State file.

Using Workspaces, the same Terraform code can provision different infrastructures for:

* Development
* Testing
* Staging
* Production

Each Workspace has its own independent State.

---

# 🎯 Why Do We Need Workspaces?

Suppose your company has three environments.

Without Workspaces:

```text id="t5w8k2"
dev/

main.tf

──────────────

staging/

main.tf

──────────────

production/

main.tf
```

Problems:

* Duplicate code
* Difficult maintenance
* Higher chance of configuration drift

With Workspaces:

```text id="k3x7n5"
main.tf

↓

Development

Testing

Production

Different State Files
```

One codebase supports multiple environments.

---

# ❌ Problems Without Workspaces

Imagine changing the EC2 instance type.

Without Workspaces:

```text id="g6p2m8"
Update Dev

↓

Update Staging

↓

Update Production

↓

Repeat
```

Maintaining multiple copies increases the risk of inconsistencies.

---

# 🏗️ Workspace Architecture

```text id="n7v4q1"
Terraform Code
       │
       ▼
Workspace
       │
 ┌─────┼─────┐
 ▼     ▼     ▼
Dev  Stage  Prod
 │     │      │
 ▼     ▼      ▼
State State  State
```

Each Workspace has its own State file while sharing the same Terraform configuration.

---

# 🌱 Default Workspace

When a Terraform project is initialized:

```bash id="v8m3k6"
terraform init
```

Terraform automatically creates a Workspace called:

```text id="r2w9p4"
default
```

If no other Workspace is selected, Terraform uses the **default** Workspace.

---

# 🚀 Creating a Workspace

Create a new Workspace:

```bash id="x5t7n1"
terraform workspace new dev
```

Create another Workspace:

```bash id="m4k9r3"
terraform workspace new production
```

Terraform automatically creates a separate State file for each Workspace.

---

# 🔄 Switching Workspaces

Switch to Development:

```bash id="c7q2v8"
terraform workspace select dev
```

Switch to Production:

```bash id="b1y6m4"
terraform workspace select production
```

Terraform loads the State file associated with the selected Workspace.

---

# 📋 Listing Workspaces

Display all available Workspaces:

```bash id="p8n4k7"
terraform workspace list
```

Example output:

```text id="j5m3x8"
default

dev

production
```

The current Workspace is marked with `*`.

---

# ❌ Deleting a Workspace

Delete a Workspace:

```bash id="r6w8p2"
terraform workspace delete dev
```

A Workspace must not be active before it can be deleted.

Switch to another Workspace first if needed.

---

# 💾 Workspace State Files

Each Workspace has its own State file.

```text id="t9q4n6"
default

↓

terraform.tfstate

──────────────

dev

↓

terraform.tfstate

──────────────

production

↓

terraform.tfstate
```

Although the Terraform code is the same, infrastructure remains isolated because each Workspace tracks its own State.

---

# ⚖️ Workspaces vs Separate Directories

| Workspaces                      | Separate Directories                            |
| ------------------------------- | ----------------------------------------------- |
| One codebase                    | Multiple copies of code                         |
| Separate State files            | Separate projects                               |
| Easy environment switching      | Manual management                               |
| Less duplication                | More duplication                                |
| Better for similar environments | Better for completely different infrastructures |

---

# ☁️ DevOps Perspective

Typical workflow:

```text id="h4v7k2"
Git Repository

↓

Terraform Code

↓

Workspace Selected

↓

terraform plan

↓

terraform apply

↓

Environment Created
```

The CI/CD pipeline selects the appropriate Workspace before deployment.

---

# 🏭 Production Example

A company manages three AWS environments.

```text id="z2m8r5"
Development

↓

Workspace: dev

──────────────

Testing

↓

Workspace: testing

──────────────

Production

↓

Workspace: production
```

Each environment:

* Uses the same Terraform code.
* Has independent infrastructure.
* Maintains its own State file.

Changing the Development environment does not affect Production.

---

# 🎯 Common Interview Questions

### What is a Terraform Workspace?

A Workspace is an isolated environment with its own Terraform State file, allowing multiple environments to use the same configuration.

---

### Which Workspace is created by default?

```text id="w7p3k9"
default
```

---

### Which command creates a new Workspace?

```bash id="q4m8r1"
terraform workspace new dev
```

---

### Which command switches Workspaces?

```bash id="n9x5v7"
terraform workspace select dev
```

---

### Which command lists all Workspaces?

```bash id="u6k2p8"
terraform workspace list
```

---

### Why are Workspaces useful?

They allow multiple environments to share the same Terraform code while maintaining separate State files.

---

# 🔍 Useful Commands

Initialize Terraform:

```bash id="f3v8n2"
terraform init
```

Create Workspace:

```bash id="a5r7m4"
terraform workspace new dev
```

List Workspaces:

```bash id="k1p9x6"
terraform workspace list
```

Show current Workspace:

```bash id="j8q2w5"
terraform workspace show
```

Switch Workspace:

```bash id="m6v4t1"
terraform workspace select production
```

Delete Workspace:

```bash id="c9r5k3"
terraform workspace delete dev
```

---

# 📑 Interview Cheat Sheet

```text id="e4n7q2"
Terraform Code
       │
       ▼
Workspace
       │
 ┌─────┼─────┐
 ▼     ▼     ▼
Dev  Stage  Prod
 │     │      │
 ▼     ▼      ▼
State State  State
```

Remember:

* **Workspaces isolate environments using separate State files**
* **Default Workspace = `default`**
* **One Terraform codebase can manage multiple environments**
* **Each Workspace has its own infrastructure state**
* **Use `terraform workspace select` to switch environments**
* **Workspaces reduce code duplication**
* **State remains isolated across environments**

---

# 📚 Summary

Terraform Workspaces provide an efficient way to manage multiple environments using a single Terraform configuration. By maintaining separate State files for each Workspace, they ensure environment isolation while reducing code duplication and simplifying infrastructure management.

For DevOps Engineers, Workspaces are valuable for managing Development, Testing, Staging, and Production environments, especially when the infrastructure is largely similar across environments.

---

# 🔗 Related Topics

⬅️ **Previous:** Modules → `../10-Modules/README.md`

➡️ **Next:** Lifecycle → `../12-Lifecycle/README.md`

### 📖 Recommended Reading

* Terraform Lifecycle
* Terraform State
* Terraform Remote State
* Terraform Modules
* Terraform Official Documentation
