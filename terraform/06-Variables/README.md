# 🔧 Terraform Variables

> **Variables in Terraform are used to make configurations reusable, flexible, and dynamic. Instead of hardcoding values directly into Terraform files, variables allow users to provide input values at runtime or from external files.**
>
> Variables help create modular Infrastructure as Code (IaC), making the same Terraform configuration usable across different environments such as Development, Testing, and Production.

---

# 📖 Table of Contents

* What are Variables?
* Why Do We Need Variables?
* Variable Architecture
* Types of Variables
* Declaring Variables
* Assigning Variable Values
* Variable Precedence
* Variable Validation
* Best Practices
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What are Variables?

A **Variable** is an input parameter used to customize Terraform configurations.

Instead of writing:

```hcl id="1a7f9d"
instance_type = "t2.micro"
```

Use:

```hcl id="9c2m4e"
instance_type = var.instance_type
```

Now the instance type can be changed without modifying the Terraform code.

---

# 🎯 Why Do We Need Variables?

Without Variables:

```text id="k5v3d2"
Development

instance_type = t2.micro

────────────────────

Production

instance_type = t3.large
```

You would need separate Terraform files.

With Variables:

```text id="v6q8n1"
Same Terraform Code

↓

Different Variable Values

↓

Different Environments
```

Benefits:

* Reusable code
* Easy customization
* Better maintainability
* Environment-specific configuration

---

# 🏗️ Variable Architecture

```text id="x9r4c7"
variables.tf
      │
      ▼
Input Variables
      │
      ▼
main.tf
      │
      ▼
Terraform Core
      │
      ▼
Provider
      │
      ▼
Infrastructure
```

Variables are declared separately and referenced wherever needed.

---

# 📂 Types of Variables

Terraform supports multiple data types.

| Type   | Example                   |
| ------ | ------------------------- |
| string | `"ap-south-1"`            |
| number | `2`                       |
| bool   | `true`                    |
| list   | `["subnet-1","subnet-2"]` |
| map    | `{env="dev"}`             |
| object | Complex structured data   |
| tuple  | Mixed ordered values      |
| set    | Unique values             |

---

# 🚀 Declaring Variables

Example:

```hcl id="r4n8k2"
variable "instance_type" {

  description = "EC2 Instance Type"

  type = string

  default = "t2.micro"
}
```

Explanation:

* **description** → Explains the variable.
* **type** → Specifies the data type.
* **default** → Optional default value.

---

# 📥 Using Variables

Reference variables using the `var` keyword.

Example:

```hcl id="b7f2y5"
resource "aws_instance" "web" {

  ami           = "ami-xxxxxxxx"

  instance_type = var.instance_type
}
```

Terraform replaces `var.instance_type` with the actual value.

---

# 📄 Assigning Variable Values

Variables can receive values in several ways.

### 1️⃣ Default Value

```hcl id="h2m5j8"
default = "t2.micro"
```

---

### 2️⃣ terraform.tfvars

```hcl id="d8x1q6"
instance_type = "t3.micro"
```

---

### 3️⃣ Command Line

```bash id="z4r7v1"
terraform apply -var="instance_type=t3.medium"
```

---

### 4️⃣ Environment Variable

```bash id="u9c6k3"
export TF_VAR_instance_type=t3.large
```

Terraform automatically reads variables prefixed with `TF_VAR_`.

---

# 📊 Variable Precedence

When multiple values are provided, Terraform follows this order (highest to lowest priority):

```text id="q7p4t8"
Command Line (-var)

↓

Environment Variables

↓

terraform.tfvars

↓

Default Value
```

The highest-priority value is used.

---

# ✅ Variable Validation

Terraform allows validation rules to ensure valid input.

Example:

```hcl id="w3m9d7"
variable "instance_count" {

  type = number

  validation {
    condition     = var.instance_count > 0
    error_message = "Instance count must be greater than zero."
  }
}
```

Validation prevents invalid configurations from being applied.

---

# 💡 Best Practices

* Keep variables in `variables.tf`
* Use meaningful variable names
* Define data types
* Add descriptions
* Use validation where possible
* Avoid hardcoding values
* Store environment-specific values in `terraform.tfvars`
* Never store secrets in plain text

---

# ☁️ DevOps Perspective

Typical project structure:

```text id="e5t8n2"
main.tf

↓

variables.tf

↓

terraform.tfvars

↓

terraform apply

↓

Infrastructure Created
```

The same Terraform code can be reused across:

* Development
* Testing
* Staging
* Production

Only the variable values change.

---

# 🏭 Production Example

A company deploys applications to three environments.

```text id="p8y4c6"
Development

instance_type = t2.micro

────────────────────

Staging

instance_type = t3.small

────────────────────

Production

instance_type = t3.large
```

All environments use the same Terraform code.

Only `terraform.tfvars` changes for each environment.

---

# 🎯 Common Interview Questions

### What are Terraform Variables?

Variables are input parameters that make Terraform configurations reusable and configurable.

---

### Where are variables usually declared?

In the `variables.tf` file.

---

### How do you reference a variable?

Using:

```hcl id="f1k7v9"
var.variable_name
```

---

### What is `terraform.tfvars`?

A file used to assign values to input variables.

---

### What is variable validation?

A feature that checks whether input values meet specified conditions before Terraform applies changes.

---

# 🔍 Useful Commands

```bash id="m4q8z1"
terraform validate

terraform plan

terraform apply

terraform apply -var="instance_type=t3.micro"

terraform apply -var-file="terraform.tfvars"
```

---

# 📑 Interview Cheat Sheet

```text id="n6r2w5"
variables.tf
      │
      ▼
terraform.tfvars
      │
      ▼
main.tf
      │
      ▼
Terraform Apply
      │
      ▼
Infrastructure
```

Remember:

* **Variables make Terraform reusable**
* **Use `var.<name>` to reference variables**
* **`variables.tf` stores variable declarations**
* **`terraform.tfvars` stores variable values**
* **Variables support multiple data types**
* **Validation improves configuration reliability**
* **Avoid hardcoding values**

---

# 📚 Summary

Variables are an essential feature of Terraform that enable reusable, maintainable, and environment-independent infrastructure code. By separating configuration from values, Variables allow the same Terraform codebase to be used across multiple environments while improving flexibility and reducing duplication.

For DevOps Engineers, mastering Variables is fundamental because nearly every production Terraform project relies on them to build scalable and configurable Infrastructure as Code.

---

# 🔗 Related Topics

⬅️ **Previous:** Resources → `../05-Resources/README.md`

➡️ **Next:** Outputs → `../07-Outputs/README.md`

### 📖 Recommended Reading

* Terraform Outputs
* Terraform State
* Terraform Modules
* HashiCorp Configuration Language (HCL)
* Terraform Official Documentation
