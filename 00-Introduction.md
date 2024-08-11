# Project Overview

When a user or developer pushes code or raises a Pull Request (PR) to GitHub, specifically to the `main` branch, it triggers a GitHub Action workflow. Here's a high-level outline of what happens next:

## Trigger Workflow
Every push or pull request to the `main` branch initiates the GitHub Action workflow.

## Build Docker Image
The workflow begins by building a Docker image from the latest code.

## Security Scan with Trivy
The built Docker image is scanned using Trivy to detect any **HIGH** or **CRITICAL** vulnerabilities.

## Publish to AWS ECR
If the image passes the security scan, it is then pushed to the AWS Elastic Container Registry (ECR) for storage.

## Kubernetes Manifest Validation
`kube-score` validates the Kubernetes YAML files to ensure they meet predefined standards and best practices.

## Deployment with Kustomize
After validation, `Kustomize` deploys the updated Kubernetes manifests to the AWS Elastic Kubernetes Service (EKS) cluster.
