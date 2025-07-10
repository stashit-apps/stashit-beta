# StashIt Unraid Template

This template allows easy installation of Stashit through Unraid's Community Applications.

## Template Structure

The Unraid template XML maps Docker environment variables and volumes to the Unraid UI:

### Path Mappings

| Unraid UI Field | Container Path | Host Path | Description |
|-----------------|----------------|-----------|-------------|
| Data Storage Path | `/app/storage` | `/mnt/user/stashit` | User files (username/collection/file) |
| Database Storage | `/app/data/postgres` | `/mnt/user/appdata/stashit/postgres` | PostgreSQL data |
| Redis Storage | `/app/data/redis` | `/mnt/user/appdata/stashit/redis` | Redis cache data |

### Environment Variable Mappings

| Unraid UI Field | Environment Variable | Default | Description |
|----------------|---------------------|---------|-------------|
| Database Password | `POSTGRES_PASSWORD` | (required) | Set on first install |
| Session Secret | `SESSION_SECRET` | (required) | Random string for encryption |
| Session Domain | `SESSION_DOMAIN` | `localhost` | Use Tailscale hostname if enabled |
| Enable Tailscale | `USE_TAILSCALE` | `true` | Secure remote access |
| Max File Size | `MAX_FILE_SIZE` | `5GB` | Upload size limit |
| Allowed Extensions | `ALLOWED_EXTENSIONS` | `*` | File type restrictions |

### Hidden/Advanced Variables

These are set automatically by the template:

- `NODE_ENV=production`
- `STORAGE_PATH=/app/storage` (internal container path)
- `DATABASE_HOST=localhost` (services run in same container)
- `REDIS_HOST=redis`
- `GOTENBERG_API_URL=http://localhost:3001`

## Installation Steps

1. **Add to Community Applications**:
   - Copy the template URL to CA
   - Or manually add the XML to `/boot/config/plugins/dockerMan/templates-user/`

2. **Configure Required Fields**:
   - Set a strong database password
   - Generate a secure session secret
   - Choose your storage share path

3. **Optional Configuration**:
   - Adjust max file size if needed
   - Set file type restrictions
   - Configure Tailscale hostname

4. **Start Container**:
   - Click Apply to create and start
   - Access via `http://[SERVER-IP]:80` or Tailscale

## File Organization

Files are automatically organized by user and collection:
```
/mnt/user/stashit/
├── john@example.com/
│   ├── Documents/
│   ├── Images/
│   └── Projects/
└── jane@example.com/
    ├── Receipts/
    └── Contracts/
```

## Tailscale Integration

When `USE_TAILSCALE=true`:
- Container registers with Tailscale
- Access via `http://stashit` on your Tailnet
- No port forwarding required
- Encrypted remote access

## Updating the Template

To update for your repository:

1. Replace repository URLs:
   - `Repository`: Your Docker Hub repo
   - `Support`: Your GitHub issues URL
   - `Project`: Your GitHub repo URL
   - `TemplateURL`: Raw GitHub URL to this XML
   - `Icon`: URL to your app icon

2. Test locally:
   - Copy to `/boot/config/plugins/dockerMan/templates-user/`
   - Install from Unraid Docker tab

3. Submit to Community Applications:
   - Fork the CA repository
   - Add your template
   - Submit pull request