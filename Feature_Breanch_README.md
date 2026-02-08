# Feature Branch Workflow – Branching Strategy

---

## 1. Introduction
In modern software development, multiple developers often work simultaneously on the same codebase. Without a clear branching strategy, this can quickly lead to conflicts, unstable builds, and production issues.

A branching strategy defines how developers create, use, and merge branches in a version control system like Git. One of the most widely used and beginner-friendly strategies is the Feature Branch Workflow.

The Feature Branch Workflow isolates new development work into separate branches called feature branches. Each feature, bug fix, or enhancement is developed independently and merged into the main codebase only after review and testing.

---

## 2. Why Feature Branch Workflow?
The Feature Branch Workflow is designed to:

- Keep the main branch stable and deployable
- Enable parallel development
- Improve code quality through reviews
- Reduce risks during development
- Support CI/CD pipelines effectively

Instead of committing directly to the main branch, developers create a new branch for each feature, bug fix, or enhancement.

---

## 3. What Is Feature Branch Workflow?
In this workflow:

- The `main` branch contains production-ready code
- Each feature or bug fix is developed in its own branch
- Feature branches are merged into `main` only after review and testing
### Branch Naming Examples
`feature/login-page`
`feature/payment-integration`
`feature/user-profile`
`bugfix/fix-null-pointer`
`hotfix/security-patch`

---

## 4. Workflow Steps
### Step 1: Step 1. Create the repository
Each new feature should reside in its own branch, which can be pushed to the central repository for backup/collaboration. But, instead of branching off of main, feature branches use develop as their parent branch. When a feature is complete, it gets merged back into develop. Features should never interact directly with main.
```bash
git checkout main
git pull origin main
git checkout -b feature/new-dashboard
```
### Step 2: Develop the Feature
- Write code
- Commit changes frequently
```bash
git status
git add .
git commit -m "Add dashboard UI"
```
### Step 3: Push Feature Branch
Push the branch to the remote repository.
```bash
git push origin feature/new-dashboard
```
### Step 4: Create Pull Request (PR)
- Open a Pull Request (PR) to merge feature/new-dashboard → main

- Team members review the code

- CI/CD pipelines may run tests automatically

### Step 5: Review & Fix
- Address review comments

- Push additional commits if needed
### Step 6: Merge to Main
Once approved:

- Feature branch is merged into main

- Feature branch is usually deleted
```bash
git checkout main
git pull origin main
git merge feature/new-dashboard
```
