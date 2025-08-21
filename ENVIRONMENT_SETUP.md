# Environment Configuration Guide

This document explains how to configure environment variables for both local development and CI/CD environments.

## 🔧 Local Development (.env files)

### Setup
1. Copy the example environment file:
   ```bash
   cp .env.example .env
   ```

2. Edit `.env` with your local settings:
   ```bash
   # Example modifications
   HOMER_PORT=8081          # Change port if 8080 is busy
   PLEX_PORT=32401          # Change port if 32400 is busy
   TZ=America/Los_Angeles   # Change timezone
   ```

3. Start services:
   ```bash
   docker compose up -d
   ```

### Benefits
- ✅ Easy local customization
- ✅ No sensitive data in repository
- ✅ Quick development iterations
- ✅ Personal preferences

## 🚀 CI/CD Environment (GitHub Secrets)

### Required Secrets
Set these in your GitHub repository settings (Settings → Secrets and variables → Actions):

| Secret Name | Description | Example Value |
|-------------|-------------|---------------|
| `TRIVY_SEVERITY` | Vulnerability severity levels | `HIGH,CRITICAL` |
| `TRIVY_VERSION` | Trivy scanner version | `0.22.0` |
| `DOCKER_COMPOSE_VERSION` | Docker Compose version | `latest` |
| `SCAN_TIMEOUT` | Scan timeout in minutes | `300` |
| `SLACK_WEBHOOK_URL` | Slack notification URL | `https://hooks.slack.com/...` |

### How It Works
1. **GitHub Actions** reads secrets automatically
2. **Environment variables** are set in workflow
3. **Secure scanning** runs with your configuration
4. **Results** are uploaded as artifacts

### Benefits
- ✅ Secure (encrypted secrets)
- ✅ Automated configuration
- ✅ Team consistency
- ✅ Production-ready

## 🔄 Environment Variable Priority

Docker Compose uses this priority order:
1. **Shell environment variables** (highest)
2. **`.env` file** in project directory
3. **Default values** in docker-compose.yml (lowest)

### Example
```bash
# Shell variable (highest priority)
export HOMER_PORT=9000
docker compose up -d

# .env file (medium priority)
# HOMER_PORT=8080

# docker-compose.yml default (lowest priority)
# ports: - "${HOMER_PORT:-8080}:8080"
```

## 🛡️ Security Best Practices

### Local Development
- ✅ Never commit `.env` files
- ✅ Use `.env.example` for documentation
- ✅ Add `.env*` to `.gitignore`
- ✅ Use non-sensitive default values

### CI/CD
- ✅ Use GitHub Secrets for sensitive data
- ✅ Rotate secrets regularly
- ✅ Use least privilege principle
- ✅ Monitor secret usage

## 🔍 Troubleshooting

### Common Issues
1. **Environment variables not loading**
   - Check `.env` file syntax
   - Verify variable names match docker-compose.yml

2. **GitHub Secrets not working**
   - Verify secret names match workflow
   - Check repository permissions

3. **Port conflicts**
   - Change ports in `.env` file
   - Check for running services

### Debug Commands
```bash
# Check environment variables
docker compose config

# View resolved configuration
docker compose config --services

# Test environment loading
env | grep HOMER
```
