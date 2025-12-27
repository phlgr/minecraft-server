# Minecraft Server (Docker Compose)

A simple Docker Compose setup for running a Purpur Minecraft server for a small private SMP (~10 players).

## Prerequisites

- Docker and Docker Compose installed
- Git

## Quick Start

```bash
# Clone this repository
git clone <your-repo-url> minecraft-server
cd minecraft-server

# Copy environment file and customize
cp .env.example .env

# Edit .env to configure your server (optional)
nano .env

# Start the server
docker compose up -d

# View logs
docker compose logs -f minecraft
```

## Configuration

### Environment Variables (.env)

Edit `.env` to customize:

- `MINECRAFT_TYPE` - Server type (PURPUR, VANILLA, PAPER, etc.)
- `MINECRAFT_VERSION` - Minecraft version or LATEST
- `MINECRAFT_PORT` - Server port (default: 25565)
- `MINECRAFT_MEMORY` - Max memory allocation (default: 2G)

### Server Configuration Files

Edit files in `data/` to customize Minecraft settings:

- `data/server.properties` - Main server configuration (difficulty, gamemode, max players, MOTD, etc.)
- `data/ops.json` - Operators/admins
- `data/whitelist.json` - Whitelisted players

**Important**: After editing configuration files, restart the server: `docker compose restart`

## Managing the Server

```bash
# Start
docker compose up -d

# Stop
docker compose stop

# Restart
docker compose restart

# View logs
docker compose logs -f minecraft

# Execute commands in server
docker compose exec minecraft rcon-cli list

# Interactive RCON session
docker compose exec -it minecraft rcon-cli

# Send command to console
docker compose exec minecraft mc-send-to-console say Hello
```

## Disaster Recovery

If the server or data is lost:

```bash
# Clone the repository
git clone <your-repo-url> minecraft-server
cd minecraft-server

# Restore from backup (if you have one)
# Or start fresh with your saved configs

# Start the server
docker compose up -d
```

**Note**: Server configuration files (server.properties, ops.json, whitelist.json) are tracked in Git, so they will be restored automatically. World data is not tracked and must be backed up separately.

## Adding Plugins

Plugins are automatically downloaded from URLs on container start.

Add plugin download URLs to `.env`:

```bash
# Edit .env
MINECRAFT_PLUGINS=""
```

### Plugin Updates

To update plugins:
1. Update the URLs in `.env`
2. Restart: `docker compose restart`
3. Plugins will auto-download (old plugins removed if `MINECRAFT_REMOVE_OLD_PLUGINS=true`)

### Plugin Configuration

Configs are auto-generated in `data/plugins/` after first run. Track reference configs in `data/plugin-configs/`.

## Troubleshooting

- Server won't start? Check logs: `docker compose logs minecraft`
- Players can't connect? Check firewall rules and port forwarding
- High memory usage? Adjust `MINECRAFT_MEMORY` in `.env`

## Resources

- [itzg/minecraft-server Docker Image](https://hub.docker.com/r/itzg/minecraft-server)
- [Purpur Documentation](https://purpurmc.org/docs)
