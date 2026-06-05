# ☁️ Multi-Environment Kubernetes Infrastructure Platform

> Production-grade cloud-native platform on AWS EKS — Terraform · ArgoCD · Helm · Prometheus · Grafana · Loki

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat&logo=kubernetes&logoColor=white)
![AWS EKS](https://img.shields.io/badge/AWS_EKS-FF9900?style=flat&logo=amazonaws&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat&logo=terraform&logoColor=white)
![ArgoCD](https://img.shields.io/badge/ArgoCD-EF7B4D?style=flat&logo=argo&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?style=flat&logo=helm&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat&logo=grafana&logoColor=white)

---

## 🎯 Overview

This project demonstrates a **production-grade Kubernetes platform** built on AWS EKS, covering the full infrastructure lifecycle from provisioning to observability. It reflects real-world patterns used in enterprise cloud-native environments: GitOps delivery, workload identity, secrets automation, and centralised monitoring.

**Key goals:**
- Multi-environment isolation (dev / staging / production)
- Zero hardcoded secrets — fully automated secrets management
- Declarative GitOps delivery with drift detection
- Full observability: metrics, logs, and alerting in one stack

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        AWS Account                          │
│                                                             │
│  ┌──────────────┐   ┌──────────────┐   ┌────────────────┐  │
│  │  dev cluster  │   │staging cluster│   │  prod cluster  │  │
│  │   (EKS)      │   │    (EKS)     │   │    (EKS)       │  │
│  └──────┬───────┘   └──────┬───────┘   └───────┬────────┘  │
│         │                  │                    │            │
│  ┌──────▼──────────────────▼────────────────────▼────────┐  │
│  │                    ArgoCD (GitOps)                     │  │
│  │         Declarative delivery · drift detection         │  │
│  └────────────────────────┬───────────────────────────────┘  │
│                           │                                  │
│  ┌────────────────────────▼───────────────────────────────┐  │
│  │               Terraform (IaC)                          │  │
│  │   VPC · EKS · IAM · IRSA · Security Groups            │  │
│  └────────────────────────────────────────────────────────┘  │
│                                                              │
│  ┌─────────────────────┐   ┌──────────────────────────────┐  │
│  │  Secrets Management  │   │      Observability Stack     │  │
│  │  External Secrets Op │   │  Prometheus · Grafana · Loki │  │
│  │  AWS Secrets Manager │   │  Fluentd · Alertmanager      │  │
│  └─────────────────────┘   └──────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

---

## 🧰 Tech Stack

| Layer | Technology |
|---|---|
| Cloud | AWS (EKS, EC2, S3, VPC, IAM) |
| Orchestration | Kubernetes, Helm |
| IaC | Terraform (modules, remote state, workspaces) |
| GitOps | ArgoCD |
| Secrets | External Secrets Operator + AWS Secrets Manager |
| Workload Identity | IRSA (IAM Roles for Service Accounts) |
| Access Control | Kubernetes RBAC, AWS IAM policies |
| Observability | Prometheus, Grafana, Loki, Fluentd, Alertmanager |
| CI/CD | GitHub Actions |

---

## ✨ Key Features

**🔐 Zero-secret workloads**
External Secrets Operator syncs secrets from AWS Secrets Manager into Kubernetes automatically. No hardcoded credentials anywhere in the cluster.

**🪪 Workload identity via IRSA**
Each Kubernetes service account is bound to a scoped AWS IAM role. Pods access AWS resources without static credentials — least-privilege by design.

**📦 GitOps delivery with ArgoCD**
All application state is declared in Git. ArgoCD continuously reconciles the cluster state, detects drift, and enables one-click rollbacks.

**📊 Centralised observability**
Full metrics (Prometheus), dashboards (Grafana), log aggregation (Loki + Fluentd), and alerting (Alertmanager) deployed across all environments.

**🔒 Multi-tenant RBAC**
Kubernetes Roles, ClusterRoles, and RoleBindings enforce namespace-level isolation between teams and environments.

---

## 📁 Repository Structure

```
.
├── terraform/
│   ├── modules/
│   │   ├── eks/           # EKS cluster + node groups
│   │   ├── vpc/           # VPC, subnets, NAT
│   │   ├── iam/           # IRSA roles and policies
│   │   └── secrets/       # Secrets Manager setup
│   ├── environments/
│   │   ├── dev/
│   │   ├── staging/
│   │   └── prod/
│   └── backend.tf         # Remote state (S3 + DynamoDB)
│
├── helm/
│   ├── apps/              # Application Helm charts
│   └── infra/             # Infrastructure charts (ESO, ArgoCD, monitoring)
│
├── argocd/
│   ├── applications/      # ArgoCD Application manifests
│   └── app-of-apps.yaml   # Root app-of-apps pattern
│
├── monitoring/
│   ├── prometheus/        # Prometheus rules and scrape configs
│   ├── grafana/           # Dashboard JSONs
│   └── loki/              # Loki + Fluentd config
│
└── .github/
    └── workflows/         # GitHub Actions CI pipelines
```

---

## 🚀 Getting Started

### Prerequisites
- AWS CLI configured with appropriate permissions
- `terraform` >= 1.5
- `kubectl` >= 1.28
- `helm` >= 3.12
- `argocd` CLI

### Deploy the infrastructure

```bash
# 1. Provision AWS infrastructure
cd terraform/environments/dev
terraform init
terraform plan
terraform apply

# 2. Configure kubectl
aws eks update-kubeconfig --name my-cluster --region eu-west-1

# 3. Bootstrap ArgoCD
kubectl apply -f argocd/app-of-apps.yaml

# 4. Verify cluster state
kubectl get nodes
kubectl get applications -n argocd
```

---

## 📊 Results

| Metric | Outcome |
|---|---|
| Environment provisioning time | Days → under 2 hours |
| Secret rotation | Manual → fully automated |
| Deployment lead time | Reduced by ~40% |
| Configuration drift | Eliminated via GitOps |

---

## 👤 Author

**Marouani Nesrine** — Cloud & Platform Engineer
📍 Tunis, Tunisia · Open to relocation in Europe
🔗 [LinkedIn](https://www.linkedin.com/in/nesrine-marouani-547651143/) · [Portfolio](https://devops-portfolio-three-liart.vercel.app/)
