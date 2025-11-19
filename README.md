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