# GitOps Strategy Documentation

---

## Document Details

| Author           | Created    | Version | Last Edited On | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ---------------- | ---------- | ------- | -------------- | ----------- | ----------- | ----------- |
| Suraj Tripathi   | 2026-02-03 | 1.0     | 2026-02-03     |Annirudh     |Shreaya S    |Ashwani     |

---

## Table of Contents
## Table of Contents
1. [Introduction](#1-introduction)
2. [What is GitOps](#what-is-gitops)
3. [Why GitOps](#why-gitops)
4. [Core GitOps Principles](#core-gitops-principles)
5. [GitOps Workflow Types](#gitops-workflow-types)
   - [Push-Based Workflow (Traditional CI/CD)](#push-based-workflow-traditional-ci-cd)
   - [Pull-Based GitOps Workflow (Recommended)](#pull-based-gitops-workflow-recommended)
6. [Workflow Comparison](#workflow-comparison)
7. [Selected GitOps Strategy](#selected-gitops-strategy)
8. [Conclusion](#conclusion)
9. [Contact Information](#contact-information)
10. [References](#references)

---

## 1. Introduction
Modern software systems demand speed, reliability, and consistency in application deployment and infrastructure management. Traditional deployment methods often rely on manual steps, scripts, or direct changes in production environments, which can lead to configuration drift, human error, and poor traceability.

GitOps is a modern operational model that uses Git as the single source of truth for infrastructure and application configuration. All changes are made via Git commits, reviewed through pull requests, and automatically applied to environments using automation tools.

This document outlines the GitOps strategies that will be implemented, including workflows, comparisons, and best practices.

---

## 2. What is GitOps?
GitOps is a set of practices that uses Git repositories to manage and automate infrastructure and application deployments.

In GitOps:
- Git is the source of truth

- Desired system state is declared (YAML/JSON/Helm)

- Automation tools continuously reconcile actual state with desired state

- Changes happen only via Git commits

In simple words: If it’s not in Git, it doesn’t exist.

Example:
```yaml
replicas: 3
image: myapp:v1
```
If someone manually changes replicas to 5, the GitOps tool will automatically revert it back to 3.

---

## 3. Why GitOps?
| Benefit | Explanation |
|------|------------|
| Single Source of Truth | Git stores the complete desired state of the system |
| Auditability & Compliance | Every change is tracked with commit history and supports easy rollback |
| Improved Security | No direct production access, PR-based approvals |
| Consistency Across Environments | Same configuration flows from Dev → QA → Prod |
| Faster Recovery | System self-heals when drift is detected |
| Automation & Scalability | Reduces manual work and human errors |

---

## 4. Core GitOps Principles

| Principle | Description |
|---------|-------------|
| Declarative Configuration | Define what the final state should be |
| Version-Controlled State | All configurations are stored in Git |
| Automated Deployments | Changes are applied automatically |
| Continuous Reconciliation | System continuously matches Git state |
| Pull-Based Delivery Model | Cluster pulls changes from Git |


---

## 5. GitOps Workflow Types
A workflow defines how changes move from Git to the actual system.
### 5.1 Push-Based Workflow (Traditional CI/CD)
Push-based workflow is a deployment method where a CI/CD pipeline pushes changes directly to the server or Kubernetes cluster.
#### How Push-Based Workflow Works (Step by Step)
- Developer commits code or configuration to Git

- CI/CD pipeline is triggered

- Pipeline runs deployment commands

- Pipeline pushes changes directly to production

Flow Representation
```bash
Developer → Git → CI/CD Pipeline → Server / Cluster
```
#### Problems with Push-Based Workflow
- CI/CD needs production access 

- Credentials are stored in CI 

- No automatic drift detection 

- Not fully secure

Because of these issues, push-based workflow is not true GitOps.

### 5.2 Pull-Based GitOps Workflow (Recommended)
#### What is Pull-Based Workflow?
In a pull-based workflow, the cluster pulls changes from Git instead of Git pushing changes to the cluster.

#### Step-by-Step Flow
- Developer updates configuration in Git

- A Pull Request is created

- Team reviews and approves the PR

- PR is merged

- GitOps tool inside the cluster pulls changes

- Changes are applied automatically

- Tool continuously checks for drift

Flow Representation
```bash
Developer → Git (PR) → GitOps Tool → Cluster
```
#### Common GitOps Tools
- Argo CD

- Flux

#### Why Pull-Based is Better

- No one pushes directly to production

- Cluster only trusts Git

- Automatic self-healing

- Strong security model

---

## 6. Workflow Comparison
|Feature|Push-Based Workflow|Pull-Based GitOps|
|-------|-------------------|-----------------|
| Deployment Method|CI pushes changes|Cluster pulls changes|
|Production Access|Required|Not required      |
|Security|Medium|High|
|Drift Detection| No | Yes  |
|Rollback| Manual|Git revert|
|Audit Trail| Partial|Complete|
|Recommended| No | Yes       |

---
## 7. Selected GitOps Strategy

We will implement the following GitOps strategy:

- Pull-based GitOps workflow

- Git as the single source of truth

- Pull Request based approvals

- No manual production changes

- Automated synchronization

### High-Level Flow

- Developer commits changes to Git

- Pull Request is reviewed and approved

- GitOps tool syncs changes automatically

- System always matches Git

---

## 8. Conclusion
GitOps is a modern and reliable way to manage deployments.

By adopting GitOps:

- Git becomes the final authority

- Manual deployments are eliminated

- Systems become predictable and secure

- Rollbacks become easy

- Infrastructure stays consistent

For modern DevOps and Kubernetes environments, GitOps is the recommended deployment strategy.

---

## 9. Contact Information

| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Name         | Suraj Tripathi                                                      |
| Role         | DevOps Trainee                                                      |
| Email        | [suraj.tripathi.snaatak@mygurukulam.co](mailto:suraj.tripathi.snaatak@mygurukulam.co) |

---
## 10. References
| Tool / Initiative | Description | Official Link |
|------------------|-------------|---------------|
| OpenGitOps | Open standard and best practices for implementing GitOps | https://opengitops.dev |
| Argo CD | Kubernetes-native GitOps continuous delivery tool | https://argo-cd.readthedocs.io |
| Flux | GitOps toolkit for Kubernetes and cloud-native apps | https://fluxcd.io/docs/ |
| CNCF GitOps | CNCF working group and GitOps ecosystem overview | https://www.cncf.io/projects/gitops/ |



