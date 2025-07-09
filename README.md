# Stashit Beta Testing Repo

🚧 **This repository contains beta releases of Stashit Self-Hosted for testing purposes.**

## ⚠️ Important Beta Testing Guidelines

  

- **Backup your data** before testing any beta version

- Beta versions may contain bugs or incomplete features

- **Do not use beta versions in production**

- Report issues in the [main repository](https://github.com/stashit-apps/stashit-self-hosted/issues)

  

## 🚀 Current Beta Version

  

The latest beta version is automatically updated when new beta releases are published.

  

Check the [main repository releases](https://github.com/stashit-apps/stashit-self-hosted/releases) to see what's new in the current beta.

  

## 📦 Unraid Installation

  

### Method 1: Template Repository (Recommended)

  

1. In Unraid, go to **Docker > Add Container**

2. Click **Template repositories**

3. Add this URL: `https://github.com/stashit-apps/stashit-beta`

4. Save, then search for "StashIt" and install

  

### Method 2: Manual Docker Pull

  

```bash

# Pull the latest beta

docker pull ghcr.io/stashit-apps/stashit-self-hosted:beta

  

# Or specific beta version

docker pull ghcr.io/stashit-apps/stashit-self-hosted:v1.3.0-beta.0

```

  

## 🐳 Docker Compose for Beta Testing

  

```yaml

version: '3.8'

services:

stashit-beta:

image: ghcr.io/stashit-apps/stashit-self-hosted:beta

container_name: stashit-beta

ports:

- "8283:80" # Different port to avoid conflicts

volumes:

- ./beta-storage:/app/storage

- ./beta-postgres:/var/lib/postgresql/data

- ./beta-redis:/data

environment:

- POSTGRES_PASSWORD=your-beta-password

- SESSION_SECRET=your-beta-session-secret

- SESSION_DOMAIN=localhost

restart: unless-stopped

```

  

## 🧪 What to Test

  

When testing beta versions, please focus on:

  

- **New features** mentioned in the release notes

- **Installation and upgrade process**

- **Performance and stability**

- **Data migration** (if applicable)

- **Compatibility** with your existing setup

  

## 🐛 Reporting Issues

  

Found a bug or have feedback?

  

1. **Search existing issues** in the [main repository](https://github.com/stashit-apps/stashit-self-hosted/issues)

2. **Create a new issue** with:

- Beta version number

- Steps to reproduce

- Expected vs actual behavior

- Your environment (Unraid version, hardware specs)

- Relevant log files

  

**Use the `beta-feedback` label** when creating issues.

  

## 📋 Beta Testing Checklist

  

Before reporting issues, please verify:

  

- [ ] You're using the correct beta image tag

- [ ] You've backed up your stable data

- [ ] The issue doesn't exist in the stable version

- [ ] You've checked the release notes for known issues

  

## 🔄 Switching Between Beta and Stable

  

### To Beta from Stable:

```bash

# Stop current container

docker stop stashit

  

# Backup your data

cp -r ./storage ./storage-backup

cp -r ./postgres ./postgres-backup

  

# Pull beta and restart

docker pull ghcr.io/stashit-apps/stashit-self-hosted:beta

# Update your docker-compose.yml or run command

```

  

### Back to Stable:

```bash

# Stop beta container

docker stop stashit-beta

  

# Restore from backup if needed

# Update to stable image

docker pull ghcr.io/stashit-apps/stashit-self-hosted:latest

```

  

## 📞 Support & Discussion

  

- **Bug Reports**: [GitHub Issues](https://github.com/stashit-apps/stashit-self-hosted/issues)

- **Questions**: [GitHub Discussions](https://github.com/stashit-apps/stashit-self-hosted/discussions)

- **Main Repository**: [StashIt Self-Hosted](https://github.com/stashit-apps/stashit-self-hosted)

  

## 🙏 Thank You!

  

Your beta testing helps make StashIt better for everyone. We appreciate your time and feedback!

  

---

  

**🔗 Quick Links:**

- [Main Repository](https://github.com/stashit-apps/stashit-self-hosted)

- [Latest Releases](https://github.com/stashit-apps/stashit-self-hosted/releases)

- [Documentation](https://github.com/stashit-apps/stashit-self-hosted/tree/main/docs)

- [Docker Images Guide](https://github.com/stashit-apps/stashit-self-hosted/blob/main/docs/DOCKER_IMAGES.md)
