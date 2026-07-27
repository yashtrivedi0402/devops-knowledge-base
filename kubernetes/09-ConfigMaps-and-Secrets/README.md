# 🔐 Kubernetes ConfigMaps & Secrets

> **ConfigMaps and Secrets are Kubernetes resources used to externalize application configuration and sensitive data from container images.**
>
> ConfigMaps store non-sensitive configuration, while Secrets securely store confidential information such as passwords, API keys, and certificates. Separating configuration from application code makes deployments more flexible, secure, and maintainable.

---

# 📖 Table of Contents

* What are ConfigMaps?
* What are Secrets?
* Why Do We Need Them?
* ConfigMap vs Secret
* How ConfigMaps Work
* How Secrets Work
* Creating ConfigMaps
* Creating Secrets
* Using ConfigMaps & Secrets
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What are ConfigMaps?

A **ConfigMap** is a Kubernetes object used to store **non-sensitive configuration data**.

Examples:

* Environment Variables
* Application Configuration
* URLs
* Feature Flags
* Configuration Files

Instead of hardcoding configuration into the application, it is stored separately in a ConfigMap.

---

# 🔐 What are Secrets?

A **Secret** stores **sensitive information** that applications require.

Examples:

* Database Passwords
* API Keys
* Authentication Tokens
* SSH Keys
* TLS Certificates

Secrets help keep confidential data separate from application code and configuration.

---

# 🎯 Why Do We Need ConfigMaps & Secrets?

Without ConfigMaps and Secrets:

```text
Application
│
├── Database Password
├── API Key
├── Database URL
├── Environment Name
└── Feature Flags
```

Problems:

* Hardcoded values
* Difficult to update
* Poor security
* Different builds for different environments

Using ConfigMaps and Secrets:

```text
Application
      │
      ├────────► ConfigMap
      │
      └────────► Secret
```

Benefits:

* Configuration can change without rebuilding the image.
* Sensitive data is managed separately.
* Easier environment management.
* Better security practices.

---

# ⚖️ ConfigMap vs Secret

| ConfigMap                     | Secret                             |
| ----------------------------- | ---------------------------------- |
| Non-sensitive data            | Sensitive data                     |
| Plain text values             | Base64-encoded values (by default) |
| Environment configuration     | Passwords, Tokens, Keys            |
| Easier to view                | Access should be restricted        |
| Used for application settings | Used for confidential information  |

> **Note:** Base64 encoding is **not encryption**. By default, Secrets are encoded for transport/storage but should be protected using RBAC, encryption at rest, and secure access controls.

---

# 🏗️ Architecture

```text
                Kubernetes Cluster
                       │
        ┌──────────────┴──────────────┐
        ▼                             ▼
   ConfigMap                      Secret
        │                             │
        └──────────────┬──────────────┘
                       ▼
                     Pod
                       │
                  Application
```

The Pod reads configuration and sensitive values at runtime.

---

# 🚀 Creating a ConfigMap

## Using YAML

```yaml
apiVersion: v1
kind: ConfigMap

metadata:
  name: app-config

data:
  APP_ENV: production
  APP_PORT: "8080"
  DB_HOST: mysql-service
```

Create it:

```bash
kubectl apply -f configmap.yaml
```

---

## Using Command Line

```bash
kubectl create configmap app-config \
  --from-literal=APP_ENV=production \
  --from-literal=APP_PORT=8080
```

---

# 🔐 Creating a Secret

## Using YAML

```yaml
apiVersion: v1
kind: Secret

metadata:
  name: db-secret

type: Opaque

data:
  username: YWRtaW4=
  password: cGFzc3dvcmQ=
```

> The values above are Base64 encoded.

Create it:

```bash
kubectl apply -f secret.yaml
```

---

## Using Command Line

```bash
kubectl create secret generic db-secret \
  --from-literal=username=admin \
  --from-literal=password=password123
```

Kubernetes automatically encodes the values before storing them.

---

# 📦 Using ConfigMaps in a Pod

Example:

```yaml
env:
- name: APP_ENV
  valueFrom:
    configMapKeyRef:
      name: app-config
      key: APP_ENV
```

The application reads the value as an environment variable.

---

# 🔒 Using Secrets in a Pod

Example:

```yaml
env:
- name: DB_PASSWORD
  valueFrom:
    secretKeyRef:
      name: db-secret
      key: password
```

The application accesses the Secret without hardcoding the password.

---

# ☁️ DevOps Perspective

In production environments:

* Application configuration is stored in ConfigMaps.
* Passwords and credentials are stored in Secrets.
* CI/CD pipelines update ConfigMaps and Secrets independently of application images.
* Access to Secrets is controlled using RBAC.
* Secrets should be encrypted at rest and rotated regularly.

Typical workflow:

```text
Git Repository
       │
       ▼
CI/CD Pipeline
       │
       ▼
Deploy Application
       │
       ├────────► ConfigMap
       │
       └────────► Secret
                │
                ▼
               Pod
```

---

# 🏭 Production Example

An online banking application needs:

Application Configuration:

```text
APP_ENV = production
LOG_LEVEL = info
DB_HOST = mysql-service
```

Stored inside a **ConfigMap**.

Database Credentials:

```text
Username = bank_admin
Password = ********
```

Stored inside a **Secret**.

When the Pod starts:

```text
Pod
 │
 ├────────► ConfigMap
 │
 └────────► Secret
        │
        ▼
Application Starts
```

The application receives both configuration and credentials without embedding them in the Docker image.

---

# 🎯 Common Interview Questions

### What is a ConfigMap?

A ConfigMap stores non-sensitive configuration data that applications can consume at runtime.

---

### What is a Secret?

A Secret stores sensitive information such as passwords, API keys, authentication tokens, and certificates.

---

### What is the difference between a ConfigMap and a Secret?

ConfigMaps store non-sensitive configuration, while Secrets store confidential information.

---

### Are Kubernetes Secrets encrypted?

By default, Secret values are Base64 encoded, **not encrypted**. Encryption at rest must be enabled separately, and access should be controlled using RBAC.

---

### Can ConfigMaps and Secrets be mounted as files?

Yes. Both can be exposed to Pods either as:

* Environment Variables
* Mounted Volumes

---

# 🔍 Useful Commands

```bash
kubectl get configmaps

kubectl describe configmap app-config

kubectl get secrets

kubectl describe secret db-secret

kubectl create configmap app-config \
  --from-literal=APP_ENV=production

kubectl create secret generic db-secret \
  --from-literal=password=password123

kubectl delete configmap app-config

kubectl delete secret db-secret
```

---

# 📑 Interview Cheat Sheet

```text
Application
      │
      ├────────► ConfigMap
      │
      │    Non-sensitive Data
      │
      └────────► Secret
           Sensitive Data
```

Remember:

* **ConfigMap = Non-sensitive configuration**
* **Secret = Sensitive information**
* **Secrets are Base64 encoded by default**
* **Never hardcode passwords in images**
* **Both can be consumed as environment variables or mounted volumes**
* **Use RBAC and encryption at rest to protect Secrets**

---

# 📚 Summary

ConfigMaps and Secrets allow Kubernetes applications to separate configuration from application code, making deployments more flexible and secure. ConfigMaps manage non-sensitive settings, while Secrets protect confidential data such as passwords and API keys.

For DevOps Engineers, mastering ConfigMaps and Secrets is essential for building secure, portable, and environment-independent deployments while following modern cloud-native best practices.

---

# 🔗 Related Topics

⬅️ **Previous:** Services → `../08-Services/README.md`

➡️ **Next:** Volumes & Persistent Storage → `../10-Volumes-and-PersistentStorage/README.md`

### 📖 Recommended Reading

* Kubernetes Volumes
* Kubernetes RBAC
* Kubernetes Secrets Best Practices
* Kubernetes Official Documentation
* Kubernetes Security Best Practices
