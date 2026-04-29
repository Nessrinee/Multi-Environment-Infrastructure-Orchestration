# Automation Orchestration

Infrastructure and deployment automation for multi-environment workloads (`prod`, `preprod`, and `test`) using Terraform, Kubernetes manifests, Helm charts, and shell utilities.

## Project Structure

- `automation_orchestration-master/prod` - production-ready infrastructure and deployment assets.
- `automation_orchestration-master/preprod` - pre-production/staging environment.
- `automation_orchestration-master/test` - test/sandbox environment.
- `automation_orchestration-master/terraform_aws_ecs_eks` - AWS ECS/EKS Terraform setup.

## Architecture Diagram

The architecture image is generated from `docs/architecture.mmd` by GitHub Actions and saved as `docs/architecture.svg`.

![Automation architecture](docs/architecture.svg)

## CI Pipeline: Generate Architecture Image

Workflow file: `.github/workflows/generate-architecture.yml`

What it does:

- triggers on push/PR changes to `README.md`, `docs/architecture.mmd`, or the workflow itself,
- uses Mermaid CLI to render `docs/architecture.mmd` to `docs/architecture.svg`,
- commits the updated SVG back to the branch automatically.

You can also run it manually from the Actions tab using `workflow_dispatch`.

## Quick Start

1. Clone the repository.
2. Choose your target environment folder under `automation_orchestration-master/`.
3. Review variables and credentials in the corresponding Terraform and Kubernetes files.
4. Apply Terraform and deploy Kubernetes/Helm resources per environment.

## Requirements

- Terraform
- kubectl
- Helm
- Access to your target Kubernetes/Cloud/On-prem environment

## Notes

- Keep secrets out of source control; use secure secret management in CI/CD.
- Review environment-specific `README.md` and checklist files before deployment.
