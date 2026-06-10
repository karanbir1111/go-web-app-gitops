# Go Web Application GitOps Infrastructure

This repository manages the declarative infrastructure and deployment configurations for the Go Web Application using GitOps principles. It serves as the single source of truth for the desired state of the application on the cloud cluster.

---

## Architecture Overview

The system architecture separates application development from infrastructure management. 

![CI/CD Pipeline Flow](https://raw.githubusercontent.com/karanbir1111/go-web-app-devops/main/CI-CD-flow.png)

---

## GitOps Workflow & Continuous Delivery

This repository drives the automated continuous delivery (CD) process:

1. **The Automation Bridge:** When the application CI pipeline completes successfully, it automatically commits an updated container image tag directly into this repository's configurations.
2. **ArgoCD Reconciliation:** The **ArgoCD Controller** continuously polls this repository for modifications.
3. **Automated Rollout:** Upon detecting a new image tag or configuration change, ArgoCD synchronizes the cluster state, applying a **Rolling Rollout** to minimize downtime.

---

## Repository Structure

The deployment configurations are organized using Kubernetes manifests and Helm charts:

* **Helm Charts:** Contains template definitions for standard, reusable deployment resources.
* **`values.yaml`:** The central configuration file defining application variables, replicas, and environments. This is the file updated by the CI pipeline bridge step to change container images.

---

## Target Environment & Infrastructure Specs

The configurations in this repository deploy and manage the following cloud architecture:

* **Orchestration Platform:** Managed **AWS EKS Cluster**.
* **Workloads:** Dual application pod deployment (`go-web-app-pod-1` and `go-web-app-pod-2`) for high availability.
* **Ingress Controller:** **Envoy Ingress Gateway** for internal cluster traffic routing and control.
* **External Access:** Provisioned **AWS Elastic Load Balancer** exposing the gateway to public web browser users.

---

## Tools Used

* **GitOps Controller:** ArgoCD
* **Package Management:** Helm
* **Container Orchestration:** Kubernetes (AWS EKS)
* **Ingress & Networking:** Envoy, AWS ELB
