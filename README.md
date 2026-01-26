## 👋 Welcome to kutt 🚀

Modern URL shortener with custom domains

## 📋 Description

Modern URL shortener with custom domains

## 🚀 Services

- **kutt**: kutt/kutt:latest

### Infrastructure Components

- **kutt-db**: Postgres database


## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/kutt/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/kutt" ~/.local/srv/docker/kutt
cd ~/.local/srv/docker/kutt
docker compose up -d
```

### Option 3: Using composemgr
```bash
composemgr install kutt
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
```

See `docker-compose.yaml` for complete list of configurable options.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:8085

## 📂 Volumes

- `./rootfs/data/kutt` - Data storage
- `./rootfs/config/kutt` - Data storage
- `./rootfs/data/db/postgres/kutt` - Data storage

## 🔐 Security

- Change all default passwords before deploying to production
- Use strong secrets for all authentication tokens
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches
- Backup your data regularly

## 🔍 Logging

```shell
docker compose logs -f kutt
```

## 🛠️ Management

```bash
# Start services
docker compose up -d

# Stop services
docker compose down

# Update to latest images
docker compose pull && docker compose up -d

# View logs
docker compose logs -f

# Restart services
docker compose restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
