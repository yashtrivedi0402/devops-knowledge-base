# 🔐 Kubernetes RBAC (Role-Based Access Control)

> **Role-Based Access Control (RBAC) is Kubernetes' authorization mechanism that controls who can access cluster resources and what actions they are allowed to perform.**
>
> RBAC helps enforce the **Principle of Least Privilege (PoLP)** by granting users, groups, or service accounts only the permissions they need, making Kubernetes clusters more secure and manageable.

---

# 📖 Table of Contents

* What is RBAC?
* Why Do We Need RBAC?
* Authentication vs Authorization
* RBAC Components
* Role vs ClusterRole
* RoleBinding vs ClusterRoleBinding
* RBAC Architecture
* Creating Roles & Bindings
* Service Accounts & RBAC
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is RBAC?

**RBAC (Role-Based Access Control)** is the authorization system in Kubernetes that determines **who can perform which actions on which resources**.

It controls access to resources such as:

* Pods
* Deployments
* Services
* ConfigMaps
* Secrets
* Nodes
* Namespaces

RBAC answers three important questions:

* **Who** is making the request?
* **What** action are they performing?
* **Which** resource are they accessing?

---

# 🎯 Why Do We Need RBAC?

Imagine a Kubernetes cluster shared by multiple teams.

```text
Development Team
Operations Team
Security Team
QA Team
```

Without RBAC:

```text
Everyone
     │
     ▼
Full Cluster Access ❌
```

Problems:

* Anyone can delete production workloads.
* Secrets can be exposed.
* Critical resources can be modified accidentally.
* Security risks increase significantly.

With RBAC:

```text
Developer
      │
      ▼
Pods & Deployments Only

Administrator
      │
      ▼
Full Cluster Access

Auditor
      │
      ▼
Read-Only Access
```

Each user receives only the permissions required for their role.

---

# 🔑 Authentication vs Authorization

Before RBAC is applied, Kubernetes performs **Authentication**.

Flow:

```text
User
 │
 ▼
Authentication
 │
 ▼
Identity Verified
 │
 ▼
Authorization (RBAC)
 │
 ▼
Allow or Deny Request
```

Difference:

| Authentication    | Authorization          |
| ----------------- | ---------------------- |
| Verifies identity | Determines permissions |
| "Who are you?"    | "What can you do?"     |
| User login        | RBAC Policies          |

---

# 🧩 RBAC Components

RBAC consists of four primary resources:

### 1️⃣ Role

Defines permissions **within a single Namespace**.

Example permissions:

* Get Pods
* Create ConfigMaps
* Delete Services

---

### 2️⃣ ClusterRole

Defines permissions **across the entire cluster**.

Examples:

* Manage Nodes
* Manage PersistentVolumes
* View Namespaces
* Cluster-wide read access

---

### 3️⃣ RoleBinding

Assigns a **Role** to:

* User
* Group
* Service Account

Within a specific Namespace.

---

### 4️⃣ ClusterRoleBinding

Assigns a **ClusterRole** across the entire cluster.

---

# ⚖️ Role vs ClusterRole

| Role                                 | ClusterRole                          |
| ------------------------------------ | ------------------------------------ |
| Namespace-scoped                     | Cluster-wide                         |
| Access to resources in one namespace | Access across all namespaces         |
| Used with RoleBinding                | Used with ClusterRoleBinding         |
| Least privilege for teams            | Administrative or shared permissions |

---

# ⚖️ RoleBinding vs ClusterRoleBinding

| RoleBinding               | ClusterRoleBinding       |
| ------------------------- | ------------------------ |
| Namespace only            | Entire cluster           |
| Binds Role or ClusterRole | Binds ClusterRole        |
| Team-specific access      | Organization-wide access |

---

# 🏗️ RBAC Architecture

```text
               User / Group / ServiceAccount
                          │
                          ▼
                 RoleBinding / ClusterRoleBinding
                          │
                          ▼
                  Role / ClusterRole
                          │
                          ▼
               Permissions (Verbs + Resources)
                          │
                          ▼
                    Kubernetes API Server
```

The API Server checks RBAC rules before allowing access to any resource.

---

# 🚀 Creating a Role

Example YAML:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role

metadata:
  name: pod-reader
  namespace: development

rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get","list","watch"]
```

Create it:

```bash
kubectl apply -f role.yaml
```

---

# 🚀 Creating a RoleBinding

Example YAML:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding

metadata:
  name: developer-access
  namespace: development

subjects:
- kind: User
  name: yash

roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

Apply it:

```bash
kubectl apply -f rolebinding.yaml
```

The user **yash** can now view Pods in the **development** namespace.

---

# 👤 Service Accounts & RBAC

Applications running inside Kubernetes Pods use **Service Accounts** instead of human users.

Example:

```text
Application Pod
       │
       ▼
Service Account
       │
       ▼
RBAC Permissions
       │
       ▼
Kubernetes API
```

Example use cases:

* Jenkins
* Argo CD
* Prometheus
* External Secrets Operator
* Custom Controllers

Each application should have its own Service Account with only the permissions it requires.

---

# ☁️ DevOps Perspective

A production Kubernetes cluster typically follows the **Principle of Least Privilege**.

Example:

```text
Developer
      │
Read Pods

────────────────────

DevOps Engineer
      │
Deploy Applications

────────────────────

Cluster Admin
      │
Full Cluster Access

────────────────────

Monitoring Tool
      │
Read Metrics Only
```

Best practices:

* Avoid using `cluster-admin` unless necessary.
* Create namespace-specific Roles.
* Use dedicated Service Accounts.
* Regularly audit RBAC permissions.
* Restrict access to Secrets.

---

# 🏭 Production Example

An organization has three teams.

```text
Development Team
        │
Manage Pods in dev namespace

Operations Team
        │
Manage Deployments in production

Security Team
        │
Read-only access across cluster
```

Architecture:

```text
Developer
     │
RoleBinding
     │
Role
     │
Development Namespace

────────────────────

Admin
     │
ClusterRoleBinding
     │
ClusterRole
     │
Entire Cluster
```

This ensures every team has only the permissions required for its responsibilities.

---

# 🎯 Common Interview Questions

### What is RBAC?

RBAC is Kubernetes' authorization mechanism that controls access to cluster resources based on assigned roles.

---

### What is the difference between Authentication and Authorization?

* **Authentication** verifies identity.
* **Authorization** determines what actions the authenticated user is allowed to perform.

---

### What is the difference between Role and ClusterRole?

* **Role:** Namespace-scoped permissions.
* **ClusterRole:** Cluster-wide permissions.

---

### What is the difference between RoleBinding and ClusterRoleBinding?

* **RoleBinding:** Grants permissions within a namespace.
* **ClusterRoleBinding:** Grants permissions across the entire cluster.

---

### Why should Service Accounts use RBAC?

Service Accounts allow applications to securely access the Kubernetes API with only the permissions they need, reducing security risks.

---

# 🔍 Useful Commands

```bash
kubectl get roles

kubectl get rolebindings

kubectl get clusterroles

kubectl get clusterrolebindings

kubectl describe role <role-name>

kubectl describe clusterrole <clusterrole-name>

kubectl auth can-i create pods

kubectl auth can-i delete deployments

kubectl apply -f role.yaml

kubectl apply -f rolebinding.yaml
```

---

# 📑 Interview Cheat Sheet

```text
Authentication
       │
       ▼
Authorization (RBAC)
       │
       ▼
Role / ClusterRole
       │
       ▼
RoleBinding / ClusterRoleBinding
       │
       ▼
Access Granted or Denied
```

Remember:

* **RBAC = Authorization mechanism**
* **Authentication happens before Authorization**
* **Role = Namespace permissions**
* **ClusterRole = Cluster-wide permissions**
* **RoleBinding = Namespace assignment**
* **ClusterRoleBinding = Cluster-wide assignment**
* **Follow the Principle of Least Privilege**
* **Use Service Accounts for applications**

---

# 📚 Summary

RBAC is the foundation of Kubernetes security, ensuring that users and applications have only the permissions they require. By combining Roles, ClusterRoles, RoleBindings, and ClusterRoleBindings, organizations can securely manage access to cluster resources while minimizing operational and security risks.

For DevOps Engineers, understanding RBAC is essential because every production Kubernetes cluster relies on it to protect workloads, sensitive data, and infrastructure from unauthorized access.

---

# 🔗 Related Topics

⬅️ **Previous:** Jobs & CronJobs → `../14-Jobs-and-CronJobs/README.md`

➡️ **Next:** Helm Basics → `../16-Helm-Basics/README.md`

### 📖 Recommended Reading

* Kubernetes Helm
* Kubernetes Service Accounts
* Kubernetes Authentication
* Kubernetes Official Documentation
* Kubernetes Security Best Practices
