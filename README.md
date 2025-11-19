# 🚀 RH1 Demo

This repository contains a comprehensive automation suite to deploy a fully integrated Internal Developer Platform (IDP) on Red Hat OpenShift. Using Ansible and GitOps principles, it provisions the entire lifecycle of the platform, from storage and identity to developer portals and observability.

  

## 🏗 The Stack

This demo orchestrates the following enterprise components:
| Category | Components | Description  |
|--|--|--|
| Orchestration | OpenShift GitOps (Argo CD)| Manages the lifecycle of all applications.|
|Identity & Access|Keycloak|Centralized SSO and Identity Management.|
|Secret Management|HashiCorp Vault + External Secrets Operator|Secure secret storage injected via External Secrets Operator|
|DevOps & CI/CD|GitLab + OpenShift Pipelines|Source code management and CI pipelines.|
|Developer Portal|Red Hat Developer Hub|Backstage-based portal for developer self-service.|
|Registry & Storage|Quay & ODF|Container registry and OpenShift Data Foundation storage.|
|Development|OpenShift Dev Spaces|Cloud-native IDE workspaces.|
|Operations|Observability & Logging|Full stack monitoring and log aggregation.|

## 🛠 Prerequisites

Before running the installation, ensure you have:

1.  **OpenShift Cluster:** Access to an OCP 4.18+ cluster with `cluster-admin` privileges.
    
2.  **System Tools:**
    
    -   Python 3.9+
    -   `oc` CLI
    -   `ansible` (Core)
        
3.  **Configuration:** Ensure your `vars/demo.yaml` is populated with your specific domain and token details.

## ⚙️ Installation Guide

The installation process is encapsulated in a Python virtual environment to ensure dependency consistency.

### 1. Clone the Repository

Bash

```
git clone https://github.com/panchoraposo/rh1-demo.git
cd rh1-demo
```

### 2. Setup Virtual Environment

Create and activate a clean Python environment to avoid conflicts.

**For Bash/Zsh:**

Bash

```
python3 -m venv venv
source venv/bin/activate
```

**For Fish Shell:**

Code snippet

```
python3 -m venv venv
source venv/bin/activate.fish
```

### 3. Install Dependencies & Run

Once the environment is active, execute the installation wrapper. This script will install required Ansible collections and python libraries before launching the playbooks.

Bash

```
./install.sh
```

> **☕ Note:** This is a full-stack deployment involving ODF, GitLab, and Vault. The complete provisioning process may take **~40 minutes** depending on your cluster's resources.

¡Tienes toda la razón! Me estaba centrando demasiado en el problema de Vault que acabamos de solucionar, pero tu `site.yaml` muestra que esto es mucho más grande: es una **Plataforma de Ingeniería completa** (IDP) con almacenamiento, registros, identidad, CI/CD y observabilidad.

Aquí tienes el `README.md` actualizado, **en inglés**, reflejando la arquitectura completa de tu demo y los pasos de instalación exactos que utilizas (virtualenv + script).

----------

# 🚀 RH1 Demo: Full Stack Platform Engineering on OpenShift

This repository contains a comprehensive automation suite to deploy a fully integrated **Internal Developer Platform (IDP)** on Red Hat OpenShift. Using **Ansible** and **GitOps** principles, it provisions the entire lifecycle of the platform, from storage and identity to developer portals and observability.

## 🏗 The Stack

This demo orchestrates the following enterprise components:

**Category**

**Components**

**Description**

**Orchestration**

**OpenShift GitOps (Argo CD)**

Manages the lifecycle of all applications.

**Identity & Access**

**Keycloak**

Centralized SSO and Identity Management.

**Secret Management**

**HashiCorp Vault + ESO**

Secure secret storage injected via External Secrets Operator.

**DevOps & CI/CD**

**GitLab**

Source code management and CI pipelines.

**Developer Portal**

**Red Hat Developer Hub (RHDH)**

Backstage-based portal for developer self-service.

**Registry & Storage**

**Quay & ODF**

Container registry and OpenShift Data Foundation storage.

**Development**

**Red Hat DevSpaces**

Cloud-native IDE workspaces.

**Operations**

**Observability & Logging**

Full stack monitoring and log aggregation.

Code snippet

```
graph TD
    User[Developer / Platform Eng] --> RHDH[Developer Hub]
    User --> DevSpaces[DevSpaces IDE]
    
    subgraph "OpenShift Platform"
        RHDH --> GitLab
        RHDH --> ArgoCD[GitOps]
        
        ArgoCD --> Vault[HashiCorp Vault]
        ArgoCD --> Keycloak
        ArgoCD --> Quay
        
        Vault -.->|ESO| Secret[K8s Secrets]
        Keycloak -.->|SSO| RHDH
        Keycloak -.->|SSO| GitLab
    end
    
    subgraph "Infrastructure"
        ODF[OpenShift Data Foundation]
        Obs[Observability/Logging]
    end

```

## 🛠 Prerequisites

Before running the installation, ensure you have:

1.  **OpenShift Cluster:** Access to an OCP 4.18+ cluster with `cluster-admin` privileges. Use this environment: [RHOAI on OCP on AWS with NVIDIA GPUs](https://catalog.demo.redhat.com/catalog?item=babylon-catalog-prod/sandboxes-gpte.ocp4-demo-rhods-nvidia-gpu-aws.prod&utm_source=webapp&utm_medium=share-link)
    
2.  **System Tools:**
    
    -   Python 3.9+
    -   `oc` CLI
    -   `ansible` (Core)
        
3.  **Configuration:** Ensure your `vars/demo.yaml` is populated with your specific domain and token details.
    

----------

## ⚙️ Installation Guide

The installation process is encapsulated in a Python virtual environment to ensure dependency consistency.

### 1. Clone the Repository

Bash

```
git clone https://github.com/panchoraposo/rh1-demo.git
cd rh1-demo
```

### 2. Setup Virtual Environment

Create and activate a clean Python environment to avoid conflicts.

**For Bash/Zsh:**

Bash

```
python3 -m venv venv
source venv/bin/activate
```

**For Fish Shell:**

Code snippet

```
python3 -m venv venv
source venv/bin/activate.fish
```

### 3. Install Dependencies & Run

Once the environment is active, execute the installation wrapper. This script will install required Ansible collections and python libraries before launching the playbooks.

Bash

```
./install.sh
```

> **☕ Note:** This is a full-stack deployment involving ODF, GitLab, and Vault. The complete provisioning process may take **20-40 minutes** depending on your cluster's resources.


## 🔧 Architecture Highlights & Fixes

This demo includes advanced configurations to solve common integration challenges:

-   **Vault & ESO Integration:** Deploys External Secrets Operator directly in the `vault` namespace to bypass complex SDN isolation issues. Includes automated `TokenReview` RBAC fixes (`system:auth-delegator`) to ensure seamless Kubernetes Authentication.
    
-   **GitOps Bootstrapping:** The installer sets up the initial Argo CD instance, which then takes over to deploy the rest of the stack (App-of-Apps pattern).
    
-   **Clean Re-installs:** The playbooks include logic to clean up orphaned Helm metadata and CRDs (specifically for ESO and Vault) to allow for safe re-runs.
    

## 📂 Project Structure

-   `playbooks/` - Main Ansible logic.
    
-   `roles/` - Modular roles for each component (`gitops-deploy-vault`, `keycloak-config`, etc.).
    
-   `vars/` - Configuration variables for the environment.
    
-   `install.sh` - Wrapper script for setup and execution.