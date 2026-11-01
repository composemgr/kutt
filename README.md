## 👋 Welcome to kutt 🚀

Self-hosted URL shortener

## 📋 Description

Kutt is a self-hosted URL shortener. It tracks per-link click statistics, lets
registered users create and manage their own links, and stores its data in
Postgres with Redis for caching.

## 🚀 Services

- **app**: kutt/kutt:latest

### Infrastructure Components

- **db**: Postgres database
- **redis**: Redis cache

## 📦 Installation

### Option 1: Quick Install

```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/kutt/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone

```bash
git clone "https://github.com/composemgr/kutt" ~/.local/srv/docker/kutt
cd ~/.local/srv/docker/kutt
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr

```bash
composemgr install kutt
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
APP_ADMIN_USER=admin
APP_SECRET_KEY=replace-with-a-random-16-byte-hex-string
DB_USER_NAME=kutt
DB_USER_PASS=replace-with-a-random-password
DB_CREATE_DATABASE_NAME=kutt
EMAIL_SERVER_HOST=172.17.0.1
EMAIL_SERVER_PORT=587
EMAIL_SERVER_MAIL_FROM=no-reply@example.com
```

See `docker-compose.yaml` for complete list of configurable options.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64229` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

The proxy variants publish no host ports. The app is reachable only through the
proxy network, and the Postgres and Redis services stay internal to the project
network in every variant.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:64229

`DEFAULT_DOMAIN` drives the domain used in generated short links, so set
`BASE_DOMAIN_NAME` to your real domain before starting the stack. The link
redirect path is served by the same container, so it needs to be reachable from
the public internet through your proxy.

## 📂 Volumes

- `./volumes/data/kutt` - Kutt data storage
- `./volumes/db/postgres/kutt` - Postgres database data
- `./volumes/db/redis/kutt` - Redis data

## 🔐 Security

- Change all default passwords before deploying to production
- Use strong secrets for all authentication tokens
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches
- Backup your data regularly

`APP_ADMIN_USER` must be listed in `ADMIN_EMAILS` to get admin rights, and that
value is built from `BASE_DOMAIN_NAME`. Registration is open by default; set
`DISALLOW_REGISTRATION` to `true` in the compose file if you want an invite-only
instance.

## 🔍 Logging

```shell
docker compose --env-file .env logs -f app
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
