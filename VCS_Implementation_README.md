# VCS(Version Control System) Implementation – Using GitHub

---

## 1. What is VCS?
VCS (Version Control System) is a system that tracks changes in source code over time.

We are using:
- Git → Version control tool
- GitHub → Remote repository hosting platform

---

## 2. Architecture Overview (Git + GitHub)
<img width="1000" height="500" alt="image" src="https://github.com/user-attachments/assets/1ace89e6-440e-4733-a9c0-09ca38631956" />

Flow:

<img width="200" height="350" alt="_- visual selection (12)" src="https://github.com/user-attachments/assets/ad5f60cf-17ff-4bd8-8886-7a633ffbefc0" />


## 3. Step-by-Step Setup VCS (GitHub)
### Step 1️⃣ Install Git
Refresh Package List:
```bash
sudo apt update
```
Install Git package
```bash
sudo apt install git -y
```
<img width="822" height="120" alt="image" src="https://github.com/user-attachments/assets/3aff4705-e828-4632-b8b1-490bf6e35a83" />

Check installation:
```bash
git --version
```
### Step 2: Configure Git (One-Time Setup)
```bash
git config --global user.name "Suraj Tripathi"
git config --global user.email "suraj.tripathi.snaatak@mygurukulam.co"
```
Verify:
<img width="1092" height="94" alt="image" src="https://github.com/user-attachments/assets/a19284d3-3b41-4a67-beb3-9df181591f2f" />

### Step 3: Create Repository on GitHub
- Login to GitHub

- Create new repository

- Name: sprint-2

- Visibility: Private/Public

- Initialize with README
<img width="804" height="500" alt="image" src="https://github.com/user-attachments/assets/a6c3d964-080f-4e23-b7fa-ffe176303877" />


### Step 4: Clone Repository to Local
```bash
git clone https://github.com/username/ot-microservices.git
cd ot-microservices
```
<img width="1098" height="208" alt="image" src="https://github.com/user-attachments/assets/477a01f5-2a33-4b3d-a416-806fa92f750d" />

This connects local system to remote GitHub repository.

---

## 4️. Branching Strategy Implemented
We followed structured branching:
|Branch|Purpose|
|------|-------|
|main|Production-ready code|
|develop|Integration branch|
|feature/*|New feature development|
|hotfix/*|Production bug fixes|

### Create Develop Branch
```bash
git checkout -b develop
git push origin develop
```
### Feature Development Flow
```bash
git checkout develop
git checkout -b feature/employee-api
```
After development:
```bash
git add .
git commit -m "feat: Added Employee API"
git push origin feature/employee-api
```

---
## 5. Pull Request Workflow
- Push feature branch

- Create Pull Request

- Assign reviewer

- Code review

- Approval

- Merge to develop

- Delete feature branch

---

## 6. Security & Governance Implementation
### Branch Protection Rules (Applied on main)
Enabled:

- Require Pull Request before merging
- Require at least 1 approval
- Restrict direct push to main
- Prevent force push

This ensures production stability.

### .gitignore Configured
To prevent committing sensitive or unnecessary files:
```bash
node_modules/
.env
*.log
dist/
```
### Commit Message Standard Followed
We used structured commit messages:
```bash
feat: new feature
fix: bug fix
docs: documentation update
refactor: code improvement
```

---

## 7. SaaS vs On-Prem VCS Comparison
|Feature|SaaS|On-Prem|
|-------|----|-------|
|Setup Time|Fast|Slow|
|Maintenance|Vendor Managed|Self Managed|
|Infra Cost|Subscription|Server + Ops Cost|
|Backup|Automatic|Manual Setup|
|Scalability|High|Limited by Infra|
|Security Control|Shared|Full Internal Control|

---

## 8. Why SaaS (GitHub) Was Selected
For this sprint:

- Faster implementation

- No infrastructure setup required

- Better collaboration

- Built-in review system

- Suitable for distributed teams



