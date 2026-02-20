# VCS(Version Control System) Implementation – Using GitHub

---

| Author | Created on | Version | Last updated by | Last edited on |  L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|-------------|-------------|-------------|
| Suraj Tripathi | 21-02-2026 | v1.0 | Suraj Tripathi | 21-02-2026  |  |  |  |

---

## Table of Contents

1. [Introduction](#1-what-is-vcs)
2. [Architecture Overview (Git + GitHub)](#2-architecture-overview-git--github)
3. [Step-by-Step Setup VCS (GitHub)](#3-step-by-step-setup-vcs-github)
   - [Install Git](#step-1-install-git)
   - [Configure Git](#step-2-configure-git-one-time-setup)
   - [Create Repository on GitHub](#step-3-create-repository-on-github)
   - [Clone Repository to Local](#step-4-clone-repository-to-local)
4. [Branching Strategy Implemented](#4-branching-strategy-implemented)
   - [Create Develop Branch](#create-develop-branch)
   - [Feature Development Flow](#feature-development-flow)
5. [Pull Request Workflow](#5-pull-request-workflow)
   - [Create Pull Request](#create-pull-request)
   - [Assign Reviewer](#assign-reviewer)
   - [Code Review](#code-review)
   - [Approval](#approval)
   - [Merge to Develop](#merge-to-develop)
   - [Delete Feature Branch](#delete-feature-branch)
6. [Security & Governance Implementation](#6-security--governance-implementation)
   - [Branch Protection Rules](#branch-protection-rules-applied-on-main)
   - [.gitignore Configuration](#gitignore-configured)
   - [Commit Message Standards](#commit-message-standard-followed)
7. [SaaS vs On-Prem VCS Comparison](#7-saas-vs-on-prem-vcs-comparison)
8. [Why SaaS (GitHub) Was Selected](#8-why-saas-github-was-selected)
9. [Contact Information](#9-contact-information)

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
```
<img width="1192" height="193" alt="image" src="https://github.com/user-attachments/assets/eb4b89dc-8615-4157-8c7e-23cd1a751e9b" />

```bash
git push origin develop
```
<img width="1381" height="73" alt="image" src="https://github.com/user-attachments/assets/7ee074f6-42fa-443d-b374-67bc51ad0b4c" />
<img width="1911" height="246" alt="image" src="https://github.com/user-attachments/assets/de6ff83a-3389-490c-919b-87e9a7dc8786" />

#### Add SSH Key to GitHub:

`GitHub → Settings → SSH and GPG Keys → New SSH Key`
<img width="1418" height="454" alt="image" src="https://github.com/user-attachments/assets/bfcbc5a7-2119-4d5b-898a-e469183f1df9" />

#### Change Remote from HTTPS to SSH
```bash
git remote -v
```
<img width="1318" height="131" alt="image" src="https://github.com/user-attachments/assets/b3ec1e5a-48e6-47c1-b068-04bb299f0dd7" />

```bash
git remote set-url origin git@github.com:suraj8957/sprint-2.git
```
verify:
<img width="1715" height="125" alt="image" src="https://github.com/user-attachments/assets/5573bc22-8182-4257-8d59-859acac17367" />
<img width="1536" height="272" alt="image" src="https://github.com/user-attachments/assets/345fe912-514d-4dcc-8f58-5bd86343a337" />
<img width="1773" height="586" alt="image" src="https://github.com/user-attachments/assets/89446471-83cd-470c-a1df-9e3818a03046" />



### Feature Development Flow
```bash
git checkout develop
```
<img width="1585" height="135" alt="image" src="https://github.com/user-attachments/assets/5482d5b7-f0f7-4b83-9a0e-b98000b7ad21" />

```bash
git checkout -b feature/employee-api
```
<img width="1669" height="216" alt="image" src="https://github.com/user-attachments/assets/efcc3b54-b5db-4970-b9cf-322e75ab394f" />

After development:
```bash
git add .
```
<img width="1887" height="400" alt="image" src="https://github.com/user-attachments/assets/f2fc3d60-992b-4cca-adb3-a38d02ad87b6" />

```bash
git commit -m "feat: Added Employee API"
```
<img width="1917" height="400" alt="image" src="https://github.com/user-attachments/assets/6c3fe343-561b-40d3-bf89-6663da8b796c" />

```bash
git push origin feature/employee-api
```
<img width="1898" height="426" alt="image" src="https://github.com/user-attachments/assets/967ed75b-47a4-45b6-8c3f-e81054283a29" />
<img width="1345" height="409" alt="image" src="https://github.com/user-attachments/assets/f8bd628a-9f42-4a5d-98f1-53e67005d432" />


---
## 5. Pull Request Workflow
- Push feature branch

- #### Create Pull Request
  <img width="1416" height="551" alt="image" src="https://github.com/user-attachments/assets/6bd813d9-4e7a-45d2-936d-f74ee8656ea3" />
  <img width="1578" height="635" alt="image" src="https://github.com/user-attachments/assets/3ab91e99-8105-40b7-b4c0-c081889c8408" />
  
  - Set Base and Compare Branch
    You will see:

        Base branch → develop (or main)

        Compare branch → feature/demo
    Make sure:
    ```bash
    base: develop
    compare: feature/demo
    ```
    <img width="1561" height="400" alt="image" src="https://github.com/user-attachments/assets/07509e60-5cf3-4c06-b60c-84f5fb38a14c" />

    - Add Details
      Title:
      ```bash
      Feature: Demo implementation
      ```
      Description:
      ```bash
      This PR adds demo feature implementation.
      Tested locally and working fine.
      ```
      <img width="1619" height="500" alt="image" src="https://github.com/user-attachments/assets/655b3df8-7eed-4056-8417-ca7814607be7" />   

- #### Assign reviewer
  - On right side: add reviewer
    
    <img width="532" height="75" alt="image" src="https://github.com/user-attachments/assets/457d49ce-5ea1-4d52-bc93-85bae44d9a4b" />

  - Add labels (optional)
    
    <img width="360" height="628" alt="image" src="https://github.com/user-attachments/assets/afd5b072-2daa-46f5-9f07-7f0f04de8a22" />


- #### Code review
  - Open the Pull Request
    - Go to your repository
    - Click on the Pull requests tab (top menu)
    - Click on the PR you want to review
      <img width="1316" height="216" alt="image" src="https://github.com/user-attachments/assets/0c4c87a9-a56c-49e6-82cf-8940bf6a7b84" />
  - Go to “Files changed” Tab
    - On the PR page, you will see these tabs:
      - Conversation
      - Commits
      - Checks
      - Files changed ✅
    Click on Files changed.

    <img width="1005" height="209" alt="image" src="https://github.com/user-attachments/assets/c53c6d34-f324-4ecd-bfa0-82434d0fc8f5" />

    Here you will see:
  
      - Green lines → Added code
      - Red lines → Removed code
      <img width="1893" height="392" alt="image" src="https://github.com/user-attachments/assets/2f9ad0b6-7bcd-4f82-b9f2-cb15da3f9322" />
  
   - Review Code Line-by-Line
     - Hover over any line
     - Click the + icon on the left
     - Write your comment
  You have two options:
    - Add single comment (immediate)
    - Start a review (for multiple comments)
  If reviewing multiple files, choose Start a review.

 - Submit Your Review
   
   After reviewing everything:
   - Click Review changes (top right)
   - Choose one option:
    <img width="1889" height="500" alt="image" src="https://github.com/user-attachments/assets/a9c4e431-4510-4798-9ff4-11d30311318b" />

- #### Approval
  <img width="1882" height="500" alt="image" src="https://github.com/user-attachments/assets/87920ecf-3552-4ad6-8e14-fb274c1c6a6b" />

- #### Merge to develop
  ```bash
  git branch
  git checkout <name of the branch you want to merge the feature branch>
  git merge <name of the feature branch>
  git pull origin develop
  git push origin develop
  ```
  <img width="1506" height="532" alt="image" src="https://github.com/user-attachments/assets/1ce0bd0d-2eb5-4826-b29a-6a70a1d23518" />
  <img width="1896" height="361" alt="image" src="https://github.com/user-attachments/assets/de8f838b-03a0-49f9-9105-cf8b8714ba4f" />
  <img width="1050" height="488" alt="image" src="https://github.com/user-attachments/assets/39b9eaa3-70b4-433a-96ea-4843c32970d8" />


- #### Delete feature branch
  ```bash
  git branch -d <name of the feature branch>  (from local)
  git push origin --delete feature/employee-api (from github repo)
  ```
  <img width="1478" height="108" alt="image" src="https://github.com/user-attachments/assets/b3687823-cc63-4e4d-b90d-cc31dbd3dcdb" />
  <img width="1381" height="158" alt="image" src="https://github.com/user-attachments/assets/2830b870-76bd-4de8-a684-0f578e93a98d" />

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

---

## 9. Contact Information
| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Name         | Suraj Tripathi                                                      |
| Role         | DevOps Trainee                                                      |
| Email        | [suraj.tripathi.snaatak@mygurukulam.co](mailto:suraj.tripathi.snaatak@mygurukulam.co) |




