#### Argo_CD Complete Notes

* Introduction to GitOps & ArgoCD
* What is GitOps ? - DVAO Principle
* why GitOps
* How GitOps Works
* GitOps vs Traditional CI/CD
* What is ArgoCD
* How ArgoCD Works
* How ArgoCD Works
* ArgoCD vs Jenkins vs FluxCD

#### Setting up ArgoCD (Local & Cloud)

* Install ArgoCD on kind Cluster
* Install ArgoCD on EKS

## What is GitOps ?

In git your keeping the all the files , like Kubernetes  YAML , Terraform , SRC code  it's like git act like single source of truth.

Avoid the manual changes in the K8s cluster.  It must be operated via git only .

**GitOps** is a modern DevOps practice that uses **Git as the single source of truth** for managing and automating infrastructure and application deployments.

Let’s break it down simply 👇

---

### ========================================

### 🧠 **Definition**

**GitOps = Git + Operations**

GitOps is a way to **deploy and manage infrastructure or applications using Git repositories** as the central control system.
In GitOps, **everything (infrastructure, app config, policies, etc.) is defined as code** and stored in a Git repository.
Then, **automation tools** continuously **synchronize the real environment** (like Kubernetes, AWS, etc.) with what’s declared in Git.

---

### ⚙️ **How GitOps Works**

1. **Define:**
   You declare your infrastructure and app configuration as code (YAML, Terraform, Helm, etc.) and store it in Git.
2. **Commit & Push:**
   You make changes by updating the code in the Git repo (like changing versions, scaling replicas, or adding resources).
3. **Automation Triggers:**
   A GitOps tool (like **Argo CD** or **Flux**) detects the change and automatically **applies it to the environment**.
4. **Sync & Reconcile:**
   The GitOps tool continuously **monitors** your cluster or cloud to ensure the **live state matches the Git state**.
   * If they drift apart (manual changes, for example), the tool can **auto-correct** the drift.

---

### 🧩 **GitOps Tools**

Common GitOps tools include:

* **Argo CD** (most popular for Kubernetes)
* **Flux CD**
* **Jenkins X**
* **Weave GitOps**
* **Spinnaker** (partially GitOps-style)

---

### 🚀 **Benefits of GitOps**


| Benefit                    | Description                                                                     |
| -------------------------- | ------------------------------------------------------------------------------- |
| **Single Source of Truth** | Everything is stored and versioned in Git.                                      |
| **Auditing & History**     | Every change is tracked in Git commits.                                         |
| **Rollback**               | Easily revert to a previous version by rolling back a commit.                   |
| **Automation**             | Continuous reconciliation ensures the system is always in the desired state.    |
| **Security**               | No need for direct access to clusters; automation tools apply changes securely. |
| **Consistency**            | Same Git config can deploy across multiple environments (dev/stage/prod).       |

---

### 🧱 **Example**

Let’s say you have a Kubernetes app.

1. You store a YAML file in Git:
   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: nginx
   spec:
     replicas: 3
     template:
       spec:
         containers:
         - name: nginx
           image: nginx:1.25
   ```
2. You commit and push it to the repo.
3. **Argo CD** detects the change and deploys the app to your Kubernetes cluster.
4. Later, you change `replicas: 5` → commit and push → Argo CD updates it automatically.

---

### 🏗️ **GitOps vs DevOps**


| Feature               | DevOps                 | GitOps                          |
| --------------------- | ---------------------- | ------------------------------- |
| **Focus**             | CI/CD pipelines        | Continuous deployment using Git |
| **Tool Example**      | Jenkins, GitLab CI     | Argo CD, Flux                   |
| **Trigger**           | Build/Deploy scripts   | Git commit                      |
| **Source of Truth**   | Multiple tools/configs | Only Git                        |
| **Environment Drift** | Manual detection       | Auto-detection and correction   |

---

Would you like me to show a **real-world GitOps example** using **Argo CD and a Kubernetes app**, step by step (from setup to auto-sync)?

### We need the controller for the K8s Cluster to see the changes, that is ArgoCD Tools , this tools always present in the K8s cluster.

### DAVO Principle

D - Declarative Files --> Manifest Files

V - Version Controlled --> VCS

A - Automated --> ArgoCD Tool

O - Obervability --> Log and Matrix visualization

## CI Action we will do it in Jenkins / GitAction

## CD Action we will do it via a ArgoCD , it pull the changes .

* Drift Detection - Continuous monitoring , auto-healing
* Auditability - Git History , Git Version
* RollBack - Checkout old git commit -> Cluster auto-roll back
* Security Model - GitOps tools run in-cluster , no external cred needed
* Source of Truth - Git Repo (helm , manifest , Kustomize )
* pipeline direction - Cluster pulls changes from git (pull)

### What is ArgoCD

Argoproj

1. ArgoCD
2. Argo RollOut
3. Argo Events
4. Argo workflow

It will do a deployment for the k8s cluster from the GitOps. By using the GitOps Principle.

### ArgoCD Architecture

ArgoCD Components

1. API Server - It manages the requests
2. Repository Server - It clone the git
3. Application Controller  - It deploy the application in K8s
