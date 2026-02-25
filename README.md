# Git-Based Deployment

This repository contains a complete Git-based deployment system with GitHub Actions CI/CD pipeline.

## Overview

This deployment system provides:
- Automated builds on push to main/develop branches
- Docker containerization
- Multi-environment deployment (staging/production)
- Automated testing
- Release management

## Quick Start

### Prerequisites
- Docker and Docker Compose
- Node.js 18+
- Git

### Local Development

1. Clone the repository:
```bash
git clone https://github.com/trajectorysubscriptions-dev/git-deployment.git
cd git-deployment
```

2. Start the application with Docker Compose:
```bash
docker-compose up -d
```

3. Access the application:
```bash
curl http://localhost:3000
```

## Deployment Workflow

### Branches
- **main**: Production deployments
- **develop**: Staging deployments
- **feature/***: Pull requests for review

### Deployment Process

1. **Push to branch** → GitHub Actions triggered
2. **Build** → Docker image built and pushed to registry
3. **Test** → Automated tests run
4. **Deploy** → Application deployed to appropriate environment
5. **Release** → Production deployments create GitHub releases

## GitHub Actions Workflows

### Deploy Application (.github/workflows/deploy.yml)

Triggers on:
- Push to main or develop
- Pull requests to main
- Manual workflow dispatch

Jobs:
- **build**: Build Docker image
- **test**: Run automated tests
- **deploy-staging**: Deploy to staging (develop branch)
- **deploy-production**: Deploy to production (main branch)

## Configuration

### Environment Variables

Create `.env` file:
```
NODE_ENV=development
DATABASE_URL=postgresql://user:password@localhost:5432/app
```

### Deployment Configuration

Edit `deployment.json` to customize:
- Environment URLs
- Resource limits
- Replica counts
- Health check settings

## Secrets

Configure these GitHub secrets for deployments:

**Staging:**
- `STAGING_DEPLOY_KEY`: SSH key for staging server
- `STAGING_DEPLOY_HOST`: Staging server hostname

**Production:**
- `PRODUCTION_DEPLOY_KEY`: SSH key for production server
- `PRODUCTION_DEPLOY_HOST`: Production server hostname

## Docker

### Build Image
```bash
docker build -t git-deployment:latest .
```

### Run Container
```bash
docker run -p 3000:3000 git-deployment:latest
```

### Push to Registry
```bash
docker tag git-deployment:latest ghcr.io/trajectorysubscriptions-dev/git-deployment:latest
docker push ghcr.io/trajectorysubscriptions-dev/git-deployment:latest
```

## Monitoring

Monitor deployments:
- GitHub Actions: https://github.com/trajectorysubscriptions-dev/git-deployment/actions
- Releases: https://github.com/trajectorysubscriptions-dev/git-deployment/releases

## Troubleshooting

### Build Failures
Check GitHub Actions logs for build errors.

### Deployment Issues
Verify secrets are configured correctly and deployment servers are accessible.

### Test Failures
Review test output in GitHub Actions workflow logs.

## Contributing

1. Create feature branch: `git checkout -b feature/your-feature`
2. Commit changes: `git commit -am 'Add feature'`
3. Push to branch: `git push origin feature/your-feature`
4. Create Pull Request

## License

MIT
