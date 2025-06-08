# OpenShift GitOps Bootstrap

This project automates the initial setup of an OpenShift GitOps environment using Argo CD, Sealed Secrets, and Ansible. Ideal for platform engineers aiming to accelerate Day 1/Day 2 cluster readiness.

## Features

- Ansible automation for:
  - Installing ArgoCD
  - Configuring sealed-secrets controller
  - Bootstrapping GitOps repo structure
- Sample apps deployed via ArgoCD
- Works on OpenShift 4.x clusters

## Prerequisites

- Access to an OpenShift cluster
- Ansible installed locally
- `oc` CLI configured and logged in
- Install required Ansible collection:
  ```bash
  ansible-galaxy collection install kubernetes.core
  ```

## Setup (Automated with Ansible)

```
ansible-playbook playbooks/bootstrap.yml -e "cluster_name=dev-cluster"
```

## Quick Test (Manual Apply)

To verify manifests before running Ansible, you can apply them directly using `oc`:

```
oc apply -f manifests/argocd-install.yaml
oc apply -f manifests/sealedsecrets-controller.yaml
```

This helps confirm your OpenShift cluster setup and RBAC is correctly configured.

## Repo Structure

```
.
├── ansible/
│   └── roles/
│       ├── argocd/
│       │   └── tasks/
│       └── sealedsecrets/
│           └── tasks/
├── playbooks/
│   └── bootstrap.yml
├── manifests/
│   ├── argocd-install.yaml
│   └── sealedsecrets-controller.yaml
└── README.md
```
