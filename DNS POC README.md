## POC: DNS(Domain Name System)

### 1. What is DNS
DNS (Domain Name System) is the "phonebook of the internet," translating human-readable domain names (e.g., example.com) into machine-readable numerical IP addresses (e.g., 192.0.2.1). It eliminates the need to memorize complex IP addresses, allowing browsers to load internet resources by mapping names to specific server location

---
#### 1.1 Key Aspects of DNS:

- **Function**: It converts domain names into IP addresses, facilitating internet navigation.
- **Structure:** It operates as a hierarchical and distributed system, comprising root servers, TLD (top-level domain) servers, and authoritative nameservers.
- **Process:** When a URL is entered, a query is sent to DNS servers to find the corresponding IP address.
- **Importance:** DNS is fundamental for internet functionality, allowing users to access websites using simple, memorable names.

---
#### 1.2 Components of a DNS Query:

- **DNS Resolver:** The server that receives the initial request from the user's computer.
- **Root Server:** The first step in translating human-readable names into IP addresses.
- **TLD Server:** Handles the top-level domain (e.g., .com, .org).
- **Authoritative Name Server:** The final step, providing the actual IP address for the domain.

![1674789713761](https://github.com/user-attachments/assets/b8573728-542a-46d4-bdf7-f99175a06f17)

---
### 2. Overview

This project demonstrates a complete Proof of Concept (POC) for:
- Purchasing a domain (example: Hostinger)
- Hosting DNS on AWS Route 53
- Mapping the domain to an application hosted on AWS EC2
- Serving traffic using Nginx

After completing this POC, the application will be accessible using a custom domain name.

---
### 3. Objective
- Buy a domain
- Point domain nameservers to Route 53
- Create DNS records in Route 53
- Map domain to EC2 public IP
- Access application using domain name
  ```bash
  Example: http://myappdemo.in
  ```
### 4. Steps to get domain

| Step | Title | Description |
|-----|------|------------|
| Step 1 | Open Hostinger Website | Open your browser, go to **https://www.hostinger.in**, and click **Domains** from the top menu. |
| Step 2 | Search for Domain Name | Enter your desired domain name (e.g. `myappdemo.in`) in the search box and click **Search**. If available, click **Add to Cart**; if not, try another name. |
| Step 3 | Select Registration Period | Choose the domain registration period (1 year recommended for POC). Keep **Domain Privacy Protection** enabled and click **Continue**. |
| Step 4 | Login or Create Account | Login to your Hostinger account or create a new one using Email or Google. Verify your email address if prompted. |
| Step 5 | Make Payment | Choose a payment method (Debit Card, Credit Card, UPI, Net Banking) and complete the payment process. |
| Step 6 | Verify Domain Ownership | Open the verification email from Hostinger and click **Verify Email / Verify Domain**. This step is mandatory to avoid domain suspension. |
| Step 7 | Confirm Domain is Active | Login to Hostinger → **Domains** and confirm the domain status shows **Active**. Click **Manage** to proceed with DNS setup. |

Note: Domain verification via email is mandatory. Without verification, DNS configuration and domain usage may not work properly.

---
### 5. Create Hosted Zone in Route 53

1. Login to AWS Console
2. Open **Route 53**
3. Go to **Hosted Zones**
4. Click **Create Hosted Zone**
5. Enter:
   - Domain name: `myappdemo.in`
   - Type: Public Hosted Zone
6. Create hosted zone

AWS will generate:
- NS records
- SOA record

---
### 6. Update Nameservers in Domain Registrar

1. Go to Hostinger → Domains → Manage
2. Open **Nameservers**
3. Select **Custom Nameservers**
4. Copy **NS records** from Route 53
5. Paste them into Hostinger
6. Save changes

<img width="1887" height="793" alt="image" src="https://github.com/user-attachments/assets/c0cba4f8-4517-4855-a87a-7ef7e5e58274" />


 Nameserver propagation may take **30 minutes to 24 hours**

 ---
 ### 7. Launch EC2 Instance

1. Login to AWS Console
2. Go to **EC2 → Launch Instance**
3. Select:
   - OS: Ubuntu 22.04
   - Instance type: t2.micro
4. Create key pair
5. Security Group:
   - SSH (22)
   - HTTP (80)
6. Launch instance
7. Copy **Public IP**

---
### 8. Install Nginx on EC2

SSH into EC2:
```bash
ssh ubuntu@<EC2_PUBLIC_IP>
```
Install Nginx:
```bash
sudo apt update
sudo apt install nginx -y
```
Verify:
```bash
curl http://localhost
```

---
### 9. Create DNS Record in Route 53

- Open Route 53 → Hosted Zone

- Click Create Record

- Configure:

#### Root Domain (A Record)

- Record name: (leave empty)

- Type: A

- Value: EC2 Public IP

- TTL: 300

#### WWW Subdomain (A Record)

- Record name: www

- Type: A

- Value: EC2 Public IP

Save records.

---
### 10. Configure Nginx for Domain
Create config:
```bash
sudo nano /etc/nginx/sites-available/myappdemo
```
```bash
server {
    listen 80;
    server_name myappdemo.in www.myappdemo.in;

    location / {
        root /var/www/html;
        index index.html;
    }
}

```
Enable configuration:
```bash
sudo ln -s /etc/nginx/sites-available/myappdemo /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

---
### 11. Validation
DNS check:
```bash
nslookup myappdemo.in
```
Browser test:
```bash
http://myappdemo.in
```

---
### 12. POC Summary
This POC demonstrates integrating a domain with AWS Route 53 by creating a public hosted zone, updating domain nameservers, configuring DNS records to point to an EC2 instance, setting up Nginx, and successfully accessing the application using the domain name.
