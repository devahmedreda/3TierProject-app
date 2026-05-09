# TaskMaster App

3-Tier Application Source Code (Frontend + Backend)

## Architecture

| Component | Technology | Port |
|-----------|-----------|------|
| Frontend | Nginx + HTML/JS | 80 |
| Backend | Node.js + Express | 8081 |
| Database | MongoDB (managed in GitOps repo) | 27017 |

## CI Pipeline

On push to `main` (when `backend/` or `frontend/` changes):

1. **Detect Changes** — Only build what changed
2. **Build & Push** — Docker build → Push to AWS ECR
3. **Update GitOps** — Update image tags in [`taskmaster-gitops`](https://github.com/devahmedreda/taskmaster-gitops) repo

> **Note:** This repo does NOT contain Kubernetes manifests.
> ArgoCD watches the [GitOps repo](https://github.com/devahmedreda/taskmaster-gitops) for deployments.

## Required GitHub Secrets

| Secret | Description |
|--------|-------------|
| `AWS_ACCESS_KEY_ID` | AWS IAM access key |
| `AWS_SECRET_ACCESS_KEY` | AWS IAM secret key |
| `GITOPS_PAT` | GitHub Personal Access Token with `repo` scope to push to the GitOps repo |

## Local Development

```bash
# Backend
cd backend
npm install
npm start

# Frontend (just open in browser)
open frontend/index.html
```
