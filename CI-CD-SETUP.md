# Rentverse AI Service - CI/CD Setup

## 🚀 Auto-Deployment Setup

This repository is configured with GitHub Actions for automatic deployment to your server.

### Prerequisites

1. **Server Requirements:**
   - Docker and Docker Compose installed
   - SSH access enabled
   - Git installed

2. **GitHub Secrets:**
   You need to configure these secrets in your GitHub repository:
   - Go to: `Settings` → `Secrets and variables` → `Actions` → `New repository secret`

### Required GitHub Secrets

| Secret Name | Description | Example |
|------------|-------------|---------|
| `SERVER_HOST` | Your server IP or domain | `34.101.99.60` |
| `SERVER_USER` | SSH username | `root` or `ubuntu` |
| `SSH_PRIVATE_KEY` | SSH private key for authentication | Your private key content |
| `SERVER_PORT` | SSH port (optional, default: 22) | `22` |
| `DEPLOY_PATH` | Path where AI service is deployed | `/opt/rentverse-ai-service` |

### How to Get SSH Private Key

```bash
# On your local machine, generate SSH key if you don't have one
ssh-keygen -t ed25519 -C "github-actions"

# Copy the PRIVATE key content (id_ed25519)
cat ~/.ssh/id_ed25519

# Copy the PUBLIC key to your server
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@your-server
```

### Server Setup (One-time)

```bash
# SSH to your server
ssh user@34.101.99.60

# Create deployment directory
sudo mkdir -p /opt/rentverse-ai-service
sudo chown $USER:$USER /opt/rentverse-ai-service

# Clone the repository
cd /opt/rentverse-ai-service
git clone https://github.com/PratamaRizki22/metaairflow-ai.git .

# Initial deployment
docker compose up -d --build
```

### Deployment Workflow

The CI/CD pipeline will automatically:

1. ✅ Trigger on push to `master` branch
2. ✅ Connect to your server via SSH
3. ✅ Pull latest code from GitHub
4. ✅ Rebuild Docker containers
5. ✅ Restart services
6. ✅ Perform health check
7. ✅ Clean up old Docker images

### Manual Deployment

You can also trigger deployment manually:
- Go to: `Actions` → `Deploy AI Service` → `Run workflow`

### Monitoring

Check deployment status:
```bash
# On your server
cd /opt/rentverse-ai-service
docker compose ps
docker compose logs -f rentverse-ai
```

### Endpoints

After deployment, your AI service will be available at:
- **Health Check:** `http://34.101.99.60/api/v1/health`
- **API Docs:** `http://34.101.99.60/docs`
- **Nginx Proxy:** `http://34.101.99.60` (port 80)

### Troubleshooting

**Deployment fails:**
```bash
# Check GitHub Actions logs
# SSH to server and check:
docker compose logs rentverse-ai
```

**Health check fails:**
```bash
# On server
curl http://localhost:8000/api/v1/health
docker compose restart rentverse-ai
```

## 📝 Environment Variables

Create `.env` file on server if needed:
```bash
DEBUG=false
LOG_LEVEL=INFO
```

## 🔒 Security Notes

- Never commit SSH private keys to repository
- Use GitHub Secrets for sensitive data
- Keep your server firewall configured properly
- Regularly update Docker images

## 📞 Support

For issues, check:
1. GitHub Actions logs
2. Server Docker logs: `docker compose logs`
3. Server system logs: `journalctl -u docker`
