# Multi-Environment Infrastructure Orchestration

> End-to-end DevOps automation project for provisioning and deploying workloads
> across `prod`, `preprod`, and `test` environments using Terraform, Kubernetes,
> Helm, and GitHub Actions.

![Terraform](https://img.shields.io/badge/IaC-Terraform-623CE4?logo=terraform)
![Kubernetes](https://img.shields.io/badge/Platform-Kubernetes-326CE5?logo=kubernetes&logoColor=white)
![Helm](https://img.shields.io/badge/Package-Helm-0F1689?logo=helm&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/CI-GitHub%20Actions-2088FF?logo=githubactions&logoColor=white)
![Status](https://img.shields.io/badge/status-active-brightgreen)

> ⚠️ **This repository is an infrastructure showcase and lab workspace.**
> Validate variables, credentials, and target clusters before any apply/deploy.

---

## 🎯 Problem

Managing infrastructure and Kubernetes delivery manually across multiple
environments leads to inconsistency, drift, and deployment risk.

This project standardizes provisioning and release workflows with reusable
Terraform modules, Kubernetes manifests, Helm charts, and CI automation.

---

## ⚙️ How it works

```bash
# Example workflow
terraform init
terraform plan
terraform apply
helm upgrade --install mpleo ./chart_helm -f values_mpleo.yml
kubectl apply -f kubernetes_file/
```

```text
[iac]       Terraform provisioning started...           network/compute ready
[cluster]   Kubernetes resources apply...              services/secrets created
[release]   Helm chart deployment...                   app rollout started
[ci]        GitHub Actions renders architecture...     docs/architecture.svg updated
```

---

## 🏗️ Architecture

The diagram is generated automatically from Mermaid source in CI.

![Automation architecture](docs/architecture.svg)

---

## 🧰 Tech stack

| Layer | Technology |
|---|---|
| Infrastructure as Code | Terraform |
| Container orchestration | Kubernetes |
| Packaging/deployment | Helm |
| CI/CD automation | GitHub Actions |
| Scripting | Shell scripts |
| Environments | prod / preprod / test |

---

## 📐 Design principles

- **Environment parity** — same deployment patterns across `prod`, `preprod`, and `test`
- **Infrastructure as code first** — reproducible infrastructure with Terraform modules
- **Composable deployments** — Kubernetes manifests and Helm charts remain modular
- **Automation over manual ops** — CI pipeline generates and tracks architecture artifacts
- **Operational clarity** — separate folders and checklists by environment

---

## 🗂️ Project structure (overview)

```text
automation_orchestration-master/
├── automation_orchestration-master/
│   ├── prod/                    # Production environment assets
│   ├── preprod/                 # Pre-production/staging assets
│   ├── test/                    # Test/sandbox assets
│   └── terraform_aws_ecs_eks/   # AWS ECS/EKS Terraform setup
├── .github/workflows/
│   └── generate-architecture.yml
└── docs/
    ├── architecture.mmd         # Mermaid source
    └── architecture.svg         # Generated diagram
```

---

## 🚀 Usage (summary)

```bash
# 1) Go to target environment
cd automation_orchestration-master/preprod

# 2) Provision infrastructure (example path)
cd Terraform_use/onprem_lab
terraform init && terraform plan && terraform apply

# 3) Deploy application resources (example path)
cd ../../kubernetes_file
kubectl apply -f .

# 4) Deploy/upgrade Helm chart (if used)
cd ../chart_helm
helm upgrade --install mpleo . -f values_mpleo.yml
```

---

## 🤖 CI pipeline (architecture image)

Workflow: `.github/workflows/generate-architecture.yml`

- Triggered on changes to `README.md`, `docs/architecture.mmd`, or workflow file
- Renders `docs/architecture.mmd` into `docs/architecture.svg` using Mermaid CLI
- Auto-commits updated diagram to keep documentation synced with architecture

---

## 👤 Author

**Marouani Nesrine** — Cloud DevOps Engineer  
📍 Tunis  
🔗 [LinkedIn](https://www.linkedin.com/in/nesrine-marouani-547651143/)

---

*Built to industrialize infrastructure provisioning and application deployment
across multiple environments with repeatable DevOps workflows.*
