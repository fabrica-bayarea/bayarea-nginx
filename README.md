# bayarea-nginx

Nginx reverse proxy gateway for all Bay Area applications deployed on EKS.

## Architecture

All traffic to `bayarea.dataiesb.com` goes through this nginx, which routes by path prefix:

| Path | Service |
|------|---------|
| `/prontuario/api/` | Prontuario Backend (prod) |
| `/prontuario/` | Prontuario Frontend (prod) |
| `/prontuario-dev/api/` | Prontuario Backend (dev) |
| `/prontuario-dev/` | Prontuario Frontend (dev) |
| `/sprint/api/` | Sprint-Tracker Backend |
| `/sprint/` | Sprint-Tracker Frontend |
| `/tutor` | Tutor static page |
| `/` | Landing page |

## Deployment

Pushes to `main` trigger automatic build and deploy via GitHub Actions → ECR → EKS.

### Required GitHub Secrets/Vars

- `BAYAREA_ROLE_ARN` — IAM role for OIDC auth
- `AWS_REGION` — (var) defaults to `us-east-1`
- `EKS_CLUSTER_NAME` — (var) cluster name
