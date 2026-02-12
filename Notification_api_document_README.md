# Notification Worker – Elasticsearch Integrated Email Service

---

| Author | Created on | Version | Last updated by | Last edited on |
|--------|------------|---------|-----------------|----------------|
| Suraj Tripathi | 12-02-2026 | v1.0 | Suraj Tripathi | 12-02-2026 |

---

## Table of Contents

1. [Purpose](#1-purpose)
2. [Pre-requisites](#2-pre-requisites)
3. [Dependencies](#3-dependencies)
4. [Architecture](#4-architecture)
5. [Workflow Diagram](#5-workflow-diagram)
6. [Step-by-Step Installation](#6-step-by-step-installation)
7. [Disaster Recovery](#7-disaster-recovery)
8. [High Availability](#8-high-availability)
9. [Troubleshooting](#9-troubleshooting)
10. [FAQ](#10-faq)
11. [Contact Information](#11-contact-information)
12. [References](#12-references)

---

# 1. Purpose

The Notification Worker is responsible for:

- Fetching employee records from Elasticsearch
- Extracting employee email IDs
- Sending automated email notifications using SMTP
- Running in either scheduled or one-time execution mode

This PoC validates:

Employee API → Elasticsearch → Notification Worker → SMTP → Employee Inbox

It demonstrates a fully operational backend-to-email automation pipeline.

---

# 2. Pre-requisites

## 2.1 System Requirements

| Component | Recommended Specification |
|------------|----------------------------|
| Processor | Dual-Core |
| RAM | 4 GB |
| Disk | 20 GB |
| Operating System | Ubuntu 22.04 LTS |

---

## 2.2 Software Requirements

| Requirement | Minimum Recommendation |
|--------------|------------------------|
| Python | 3.8+ |
| Elasticsearch | 7.x / 8.x |
| Go | 1.20+ (for Employee API) |
| SMTP Provider | Gmail (App Password enabled) |

---

# 3. Dependencies

## 3.1 Run-time Dependencies

| Dependency | Version | Description |
|--------------|----------|-------------|
| Python | 3.x | Runtime for worker |
| Elasticsearch | 7.x/8.x | Data source |
| OpenSSL | 1.1+ | Secure SMTP communication |

Install required Python packages:

```bash
pip3 install elasticsearch schedule pyyaml
```
## 3.2 Important Ports

|port|Direction|Description|
|----|---------|-----------|
|9200|Internal|Elasticsearch
|587|Outbound|Gmail SMTP|
|8080|Internal|Employee API|

---

# 4. Architecture
<img width="1090" height="246" alt="_- visual selection (1)" src="https://github.com/user-attachments/assets/6a1f2a68-7776-4b00-91e2-8d09141578c3" />
