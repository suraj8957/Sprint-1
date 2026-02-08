# POC: SSL Certificate

## Document Details
|     Author      |  Created on  | Version |  Pre Reviewer  | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|-----------------|--------------|---------|----------------|-------------|-------------|-------------|
| Suraj Tripathi  |  04-02-2026  |  1.0    |                |  Aniruddh   |   Shreya S  |    Ashwani  |


## Purpose of this Document
This document explains what SSL is, why it is needed, and how to install and issue an SSL certificate on a domain using a free and trusted Certificate Authority.

## What is SSL?
SSL (Secure Sockets Layer) is a security technology that:
- Encrypts data between user browser and server
- Protects sensitive information (passwords, data, forms)
- Converts `http://` into `https://`
### Without SSL
`User ---> Server
(Data is readable)`
### With SSL
`User ---> 🔒 Encrypted Data 🔒 ---> Server`

---
## What is HTTPS?
- **HTTP** = Not secure  
- **HTTPS** = Secure (HTTP + SSL)
If a website has SSL:
- Browser shows 🔒 lock icon
- URL starts with `https://`

---
## Why SSL is Important?
- Protects user data
- Prevents hacking & data sniffing
- Required for login forms & payments
- Google prefers HTTPS websites (SEO benefit)

---
## 🧾 What is an SSL Certificate?
An **SSL certificate** is a digital file that:
- Proves ownership of a domain
- Enables encryption
- Is issued by a trusted authority

---
## Who Issues SSL Certificates?
SSL certificates are issued by **Certificate Authorities (CA)**.

In this POC, we use:
- Let's Encrypt: A free and trusted Certificate Authority that issues SSL certificates (you can choose Cloudflare,ZeroSSL/SSL)
- Certbot: A command-line tool used to request, install, and renew SSL certificates

---
## SSL POC Architecture
<img width="300" height="300" alt="_- visual selection" src="https://github.com/user-attachments/assets/671e634b-8e22-409c-8cb6-1ef1cce46c34" />

---
## Pre-requisites
Before starting SSL installation, ensure:
- A domain name (example.com)
- Domain A record pointing to server public IP
- Server with public IP (VM / EC2)
- Ubuntu OS (20.04 or 22.04 recommended)
- Ports 80 and 443 open

### Verify Domain Points to Server
```bash
nslookup example.com
```
Expected output:
`example.com -> SERVER_PUBLIC_IP`
Note: If IP does not match, SSL will FAIL.

### Install Nginx Web Server
Update system:
```bash
sudo system update
```
Install Nginx:
```bash
sudo apt install nginx -y
```
Start & enable Nginx:
```bash
sudo systemctl start nginx
```
```bash
sudo systemctl enable nginx
```
Test in browser:
```bash
http://example.com
```
You should see Nginx Welcome Page.
### Install Certbot (SSL Tool)
Certbot is used to:
- Request SSL certificate

- Install SSL automatically

- Renew SSL automatically
Install Certbot:
```bash
sudo apt install certbot python3-certbot-nginx -y
```
Verify:
```bash
certbot --version
```
### Generate & Install SSL Certificate
Run:
```bash
sudo certbot --nginx -d example.com -d www.example.com
```
Certbot will ask:

Email address

Accept Terms → Yes

HTTP to HTTPS redirect → Yes
<img width="1890" height="523" alt="image" src="https://github.com/user-attachments/assets/56ae5535-06aa-4f79-a544-5087da7c60bf" />
<img width="1859" height="842" alt="image" src="https://github.com/user-attachments/assets/53d82558-92fd-4a4d-ba27-412bdf4ce46e" />
<img width="1512" height="280" alt="image" src="https://github.com/user-attachments/assets/b5b4f04c-41fd-41cb-a0c9-e2782a41b2d4" />


#### What Certbot Does Automatically
- Verifies domain ownership

- Generates SSL certificate

- Configures Nginx

- Enables HTTPS

- Adds auto-renewal

### Verify SSL Installation
Open in browser:
```bash
https://example.com
```
You should see:

- Lock icon

- HTTPS enabled

- Certificate issued by Let’s Encrypt
Command line check:
```bash
openssl s_client -connect example.com:443
```
#### Where SSL Files are Stored
SSL files location:
```bash
/etc/letsencrypt/live/example.com/
```
Important files:

- `fullchain.pem → Certificate`

- `privkey.pem → Private key`
### Auto-Renewal Test
Let’s Encrypt SSL is valid for 90 days.
Test renewal:
```bash
sudo certbot renew --dry-run
```
<img width="1709" height="341" alt="image" src="https://github.com/user-attachments/assets/ebee9b45-75fe-4146-a166-d0c099db3326" />

If no errors → Auto-renew is working.

---
## Common Problems & Fixes
|      Common Problems        |             Fixes                  |
|-----------------------------|------------------------------------|
|Domain not pointing to server|Fix DNS A record|
|Port 80/443 blocked          |sudo ufw allow 80,sudo ufw allow 443|
|Nginx config error           |sudo nginx -t|

---
## POC Conclusion
- This POC demonstrates how to:

- Understand SSL from basics

- Install free SSL using Let’s Encrypt

- Secure a domain with HTTPS

- Enable automatic certificate renewal

---
## Reference Links

- https://letsencrypt.org/docs/

- https://certbot.eff.org/

## Contact Information

| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Name         | Suraj Tripathi                                                      |
| Role         | DevOps Trainee                                                      |
| Email        | [suraj.tripathi.snaatak@mygurukulam.co](mailto:suraj.tripathi.snaatak@mygurukulam.co) |

### END of POC
