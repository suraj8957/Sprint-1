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

# 5. Step-by-Step Installation

## 5.1 Elasticsearch Deployment

**Version:** 7.8.0  
**Installation Path:** `/home/ubuntu/elasticsearch-7.8.0`  
**Service Manager:** systemd  
**Port:** 9200  
**Access Scope:** Internal VPC 

### systemd Service File
Location: `/etc/systemd/system/elasticsearch.service`
### Key Configuration
- Runs as `ubuntu` user
- Restart policy enabled
- `network.host: 0.0.0.0`
- `http.port: 9200`
- Custom `path.data` configured
### Service Commands
```bash
sudo systemctl daemon-reload
sudo systemctl enable elasticsearch
sudo systemctl start elasticsearch
sudo systemctl status elasticsearch
```
### Validation
```bash
curl http://10.0.1.25:9200
curl http://10.0.1.25:9200/_cat/indices?v
```
Elasticsearch cluster reachable and index confirmed.

## 5.2 Employee API Integration
Modified File
```bash
employee-api/api/api.go
```
Updated Function
```bash
CreateEmployeeData()
```
Logic Implemented
Upon receiving an employee creation request:

Initialized Elasticsearch client (go-elasticsearch/v7)

Indexed employee document into:
```bash
employee-management
```
Indexed Fields
- name

- email_id

- status
Dependency Installation
```bash
go get github.com/elastic/go-elasticsearch/v7
go mod tidy
```
Employee API managed via:
```bash
employee-api.service
```

## 5.3 Manual Elasticsearch Validation
Insert Test Document
```bash
curl -X PUT "http://10.0.1.25:9200/employee-management/_doc/EMP001" \
  -H "Content-Type: application/json" \
  -d '{
    "email_id": "abhinavsikarwar011@gmail.com",
    "name": "John Doe"
  }'
```
<img width="1600" height="199" alt="image" src="https://github.com/user-attachments/assets/f948ac8f-98d7-4391-af51-918a642ad033" />
<img width="1000" height="504" alt="Email Screenshot 1" src="https://github.com/user-attachments/assets/0121b8b2-62b4-4361-99f9-bc43081f8292" />

Fetch All Documents
```bash
curl -X GET "http://10.0.1.25:9200/employee-management/_search?pretty" \
  -H "Content-Type: application/json" \
  -d '{
    "query": {
      "match_all": {}
    }
  }'
```
<img width="1600" height="746" alt="image" src="https://github.com/user-attachments/assets/fdad9a00-acb3-46fd-bcc2-ff2c1a0f718c" />
Confirms:
- Index exists

- Document stored correctly

- `email_id` available for worker consumption

## 5.4 Notification Worker Setup
Location:
```bash
notification-worker/notification_api.py
```
Execution Modes
- external → One-time execution

- scheduled → Periodic polling

Testing Configuration:
```bash
schedule.every(1).minutes.do(send_mail_to_all_users)
```
Elasticsearch Query Used
```bash
index = "employee-management"
query = match_all
```
Worker extracts:
```bash
data["_source"]["email_id"]
```
Run Worker
```bash
python3 notification_api.py -m external
```
And triggers SMTP email delivery.

## 5.5 SMTP Configuration

* **Provider:** Gmail
* **Port:** 587
* **TLS:** Enabled
* **Authentication:** Gmail App Password
* **Config Source:** `NOTIFICATION_CONFIG` environment variable

Connectivity validated using:

```bash
telnet smtp.gmail.com 587
```

---

## 5.6 End-to-End Validation

### Step 1 – Create Employee

POST request to:

```
/api/v1/employee/create
```

Result:

* Document indexed into Elasticsearch

Validated via:

```bash
curl http://<ES-IP>:9200/employee-management/_search?pretty
```

---

### Step 2 – Execute Notification Worker

```bash
python3 notification_api.py -m external
```

Observed:

* Successful ES connection
* Successful query execution
* Successful SMTP authentication
* No runtime errors

---

### Step 3 – Email Delivery Confirmation

Email successfully received at the configured recipient address.

#### Verified Details:

* **Subject:** Salary Slip
* **Body:** "Your salary slip is generated please check"
* **Sender:** Configured SMTP account
* **Timestamp:** Matches worker execution time

**Screenshot Attached as Proof of Delivery**

<img width="1241" height="587" alt="image" src="https://github.com/user-attachments/assets/58752d0c-d8ab-41b6-b0b6-b186a2670613" />

<img width="744" height="485" alt="Email Screenshot 2" src="https://github.com/user-attachments/assets/373d71d8-376d-467f-b218-b72673d9824b" />

---

#### Validation Confirms

* Successful Elasticsearch data retrieval
* Proper SMTP transmission
* Email delivery to recipient inbox
* Fully operational application-to-inbox pipeline



---

## 6. Disaster Recovery
- Elasticsearch data stored locally

- systemd restart policy enabled

- SMTP credentials configured via NOTIFICATION_CONFIG

Recovery Steps:

- Restart Elasticsearch

- Restart employee-api.service

- Re-run notification worker

---

## 7. High Availability
Current PoC setup:

- Single Elasticsearch node

- Poll-based worker model

- No clustering configured

---

## 8. Troubleshooting
|Issue|Resolution|
|-----|----------|
|Elasticsearch not reachable|Verify service status|
|SMTP authentication failed|Verify Gmail App Password|
|Email not received|Check worker logs|
|Duplicate emails|Due to match_all query|

Logs verified using:
```bash
journalctl -u employee-api.service
journalctl -u elasticsearch
```

---

## 9. FAQ
|Question|Answer|
|Is this production ready?|PoC level|
|Does it support scheduling?|Yes|
|Is Elasticsearch publicly accessible?|No (Internal VPC only)|
|Does it use event-driven architecture?|No (Poll-based model)|

---

## 10. Contact Information
| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Name         | Suraj Tripathi                                                      |
| Role         | DevOps Trainee                                                      |
| Email        | [suraj.tripathi.snaatak@mygurukulam.co](mailto:suraj.tripathi.snaatak@mygurukulam.co) |

---

## 11. References
|Reference|Link|
|--------|-----|
|OT-MICROSERVICES Repo|https://github.com/OT-MICROSERVICES|
