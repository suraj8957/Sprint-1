# Notification Worker Integration with Elasticsearch

---

| Author | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Suraj Tripathi | 12-02-2026 | v1.0 | Suraj Tripathi | 12-02-2026 |  |  |  |  |

---

## Table of Contents

1. [Purpose](#1-purpose)
2. [Pre-requisites](#2-pre-requisites)
3. [Dependencies](#3-dependencies)
4. [Architecture](#4-architecture)
5. [Step-by-Step Installation](#5-step-by-step-installation)
6. [Disaster Recovery](#6-disaster-recovery)
7. [High Availability](#7-high-availability)
8. [Troubleshooting](#8-troubleshooting)
9. [FAQ](#9-faq)
10. [Contact Information](#10-contact-information)
11. [References](#11-references)

---

# 1. Purpose

Implement and validate an end-to-end notification system where:

- Employee records are indexed into Elasticsearch.
- A scheduled notification worker consumes employee data.
- Email alerts are sent via SMTP.

This PoC demonstrates:

Employee API → Elasticsearch → Notification Worker → SMTP → Inbox

Successful infrastructure provisioning, application integration, and email delivery validation.

---

# 2. Pre-requisites

## 2.1 System Requirements

| Component | Specification |
|------------|--------------|
| Operating System | Ubuntu 22.04 LTS |
| RAM | 4 GB |
| Disk | 20 GB |
| Access Scope | Internal VPC |
---

## 2.2 Software Requirements

| Software | Version |
|----------|----------|
| Elasticsearch | 7.8.0 |
| Python | 3.x |
| Go | For Employee API |
| systemd | Service management |

---

# 3. Dependencies

## 3.1 Run-time Dependencies

| Dependency | Description |
|------------|-------------|
| Elasticsearch | Data source |
| Gmail SMTP | Email transmission |
| Python schedule library | Periodic polling |

## 3.2 Important Ports

| Port | Description |
|------|-------------|
| 9200 | Elasticsearch |
| 587 | Gmail SMTP |
| 8080 | Employee API |

---

# 4. Architecture

## 4.1 Architecture Diagram

<img width="472" height="258" alt="Architecture Diagram" src="https://github.com/user-attachments/assets/93f4a32b-94cc-4e0f-9ad7-d36a878b0dba" />

---
## 4.2 Data Flow
<img width="768" height="486" alt="_- visual selection (2)" src="https://github.com/user-attachments/assets/b55b1d46-7d46-4593-8e48-b004406d7707" />


---

# 5. Workflow Diagram

## 5.1 Notification Worker Flow

