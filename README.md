# CI/CD Pipeline Project (Docker + Terraform)

## Overview

This project is a simple CI/CD setup built using GitHub Actions.

The goal was to:
- Automatically build and push a Docker image
- Automatically check Terraform code for formatting and syntax issues

Everything runs on push and pull request events, so changes are validated straight away without doing anything manually.

---

## What’s Included

### 1. Docker Pipeline (CD)

This workflow:
- Builds a Docker image from the Dockerfile
- Logs into Docker Hub using GitHub Secrets
- Pushes the image to Docker Hub

Image is published to:

pinscher90/helloapp:latest

#### Trigger
Runs on push to `main`, but only when:
- `Dockerfile` changes
- files inside `/app` change

---

### 2. Terraform Pipeline (CI)

This workflow is focused on code quality for Terraform.

It runs the following checks:
- `terraform fmt -check` → ensures consistent formatting
- `terraform init` → prepares Terraform
- `terraform validate` → checks syntax and structure

#### Trigger
Runs when:
- files inside `terraform-challenge/` change
- a pull request is opened/updated

---

## Project Structure

helloapp-cicd/
├── app/
│   └── index.html
├── Dockerfile
├── terraform-challenge/
│   └── main.tf
└── .github/
    └── workflows/
        ├── docker.yml
        └── terraform.yml

---

## Key Concepts

### CI (Continuous Integration)
The Terraform workflow acts as CI:
- runs automatically on changes
- checks code quality
- fails if formatting or syntax is incorrect

### CD (Continuous Delivery)
The Docker workflow acts as CD:
- builds the application image
- pushes it to Docker Hub automatically

---

## Testing the Pipeline

Terraform pipeline was tested by:

1. Pushing valid code → pipeline passed  
2. Breaking indentation → pipeline failed on `terraform fmt -check`  
3. Fixing formatting → pipeline passed again  

This confirms the checks are working as expected.

---

## Why This Matters

- No need to manually build or push Docker images  
- Terraform errors are caught early  
- Enforces consistent code style across the project  
- Prevents bad changes from going unnoticed  

---

## Improvements (Next Steps)

Some things that could be added:

- Run workflows on all pull requests with branch protection  
- Add version tagging for Docker images (not just `latest`)  
- Add `terraform plan` step for deeper validation  
- Deploy the container automatically to a server or cloud service  

---

## Summary

This project shows a basic but realistic CI/CD setup using:

- GitHub Actions  
- Docker  
- Terraform  

It separates responsibilities clearly:
- Docker pipeline handles delivery  
- Terraform pipeline handles validation  

Both run automatically and help maintain a clean and reliable workflow.
