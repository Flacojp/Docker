# Docker DevSecOps Repository

This repository contains Docker Compose configurations for various applications with integrated security practices and CI/CD workflows. It's designed as a learning environment for DevSecOps engineers to understand container security, automated testing, and deployment best practices.

## 🎯 Learning Objectives

This repository demonstrates:
- **Container Security**: Automated vulnerability scanning with Trivy
- **CI/CD Pipelines**: GitHub Actions workflows for testing and deployment
- **Infrastructure as Code**: Docker Compose for reproducible environments
- **Monitoring**: Slack notifications for deployment events
- **Best Practices**: Security-first container configurations

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- [Docker](https://docs.docker.com/get-docker/) (v20.10+)
- [Docker Compose](https://docs.docker.com/compose/install/) (v2.0+)
- [Git](https://git-scm.com/downloads)
- [GitHub CLI](https://cli.github.com/) (optional, for repository management)

## 🚀 Quick Start

### 1. Clone the Repository
```bash
git clone <your-repository-url>
cd <repository-name>
```

### 2. Environment Setup
Create a `.env` file in the root directory:
```bash
cp .env.example .env
# Edit .env with your specific configurations
```

### 3. Deploy Applications
```bash
# Deploy all services
docker-compose up -d

# Or deploy individual services
cd Apps/homer && docker-compose up -d
cd Apps/plex && docker-compose up -d
```

## 📁 Project Structure

```
.
├── Apps/                          # Application configurations
│   ├── homer/                     # Homer dashboard
│   │   └── docker-compose.yml     # Homer service configuration
│   └── plex/                      # Plex media server
│       └── docker-compose.yml     # Plex service configuration
├── .github/                       # GitHub Actions workflows
│   └── workflows/
│       ├── linter.yaml           # Code linting workflow
│       ├── runner_pull.yaml      # Runner management
│       ├── slack-notify.yaml     # Slack notifications
│       └── trivy.yml            # Security scanning
├── README.md                     # This file
├── SECURITY.md                   # Security policy
├── .env.example                  # Environment variables template
└── docker-compose.yml           # Main orchestration file
```

## 🔒 Security Features

### Automated Vulnerability Scanning
- **Trivy Integration**: Scans all Docker images for known vulnerabilities
- **Severity Levels**: Focuses on HIGH and CRITICAL vulnerabilities
- **Automated Workflow**: Runs on every push and pull request

### Security Best Practices
- Non-root user execution
- Minimal base images
- Regular security updates
- Network isolation
- Resource limits

## 🛠️ Available Services

### Homer Dashboard
- **Purpose**: Web-based dashboard for organizing your services
- **Port**: 8080
- **Access**: http://localhost:8080
- **Features**: 
  - Service bookmarks
  - Customizable themes
  - Responsive design

### Plex Media Server
- **Purpose**: Media streaming and organization
- **Port**: 32400
- **Access**: http://localhost:32400
- **Features**:
  - Media library management
  - Remote access
  - Multiple device support

## 🔄 CI/CD Workflows

### 1. Security Scanning (`trivy.yml`)
- **Trigger**: Push to any branch, pull requests to main
- **Purpose**: Scan Docker images for vulnerabilities
- **Tools**: Trivy vulnerability scanner
- **Output**: Security report in GitHub Actions

### 2. Slack Notifications (`slack-notify.yaml`)
- **Trigger**: Push to any branch
- **Purpose**: Notify team of deployment events
- **Configuration**: Requires `SLACK_WEBHOOK_URL` secret

### 3. Code Linting (`linter.yaml`)
- **Trigger**: Pull requests
- **Purpose**: Ensure code quality and consistency
- **Tools**: Various linting tools for different file types

## 🐛 Troubleshooting

### Common Issues

#### Port Conflicts
```bash
# Check what's using a port
sudo lsof -i :8080

# Stop conflicting service
docker stop <container_name>
```

#### Permission Issues
```bash
# Fix file permissions
sudo chown -R $USER:$USER ./Apps/

# Fix Docker socket permissions
sudo usermod -aG docker $USER
```

#### Volume Mount Issues
```bash
# Check volume status
docker volume ls

# Inspect volume contents
docker run --rm -v volume_name:/data alpine ls /data
```

### Logs and Debugging
```bash
# View service logs
docker-compose logs -f service_name

# Check container status
docker-compose ps

# Execute commands in running container
docker-compose exec service_name /bin/bash
```

## 📚 Learning Resources

### DevSecOps Concepts
- [OWASP Container Security](https://owasp.org/www-project-container-security/)
- [Docker Security Best Practices](https://docs.docker.com/develop/security/)
- [Trivy Documentation](https://aquasecurity.github.io/trivy/)

### Docker Compose
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [Compose File Reference](https://docs.docker.com/compose/compose-file/)

### GitHub Actions
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Security Hardening for Actions](https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions)

## 🤝 Contributing

### Development Workflow
1. Fork the repository
2. Create a feature branch: `git checkout -b feature/<your-username>-feature`
3. Make your changes
4. Test locally: `docker-compose up -d`
5. Run security scan: `trivy image <image_name>`
6. Commit with descriptive message: `git commit -m "Add amazing feature"`
7. Push to branch: `git push origin feature/amazing-feature`
8. Create a Pull Request

### Commit Message Convention
```
type(scope): description

Examples:
feat(homer): add custom theme support
fix(plex): resolve volume mount issue
docs(readme): update installation instructions
security(trivy): update to latest version
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

- **Issues**: [GitHub Issues](https://github.com/<your-username>/<repo-name>/issues)
- **Discussions**: [GitHub Discussions](https://github.com/<your-username>/<repo-name>/discussions)
- **Security**: [Security Policy](SECURITY.md)

---

