# Purpur Minecraft Server - Ansible Deployment

Deploy a Purpur Minecraft server on Ubuntu/Debian using Ansible and Docker.

## Prerequisites

- Ansible installed
- SSH access to target server (Ubuntu/Debian)
- `community.docker` collection: `ansible-galaxy collection install -r requirements.yml`

## Quick Start

1. **Configure inventory** (`inventory/hosts.yml`):
```yaml
---
minecraft_servers:
  hosts:
    minecraft-server-1:
      ansible_host: YOUR_SERVER_IP
      ansible_user: ubuntu
      ansible_port: 22
```

2. **Configure variables** (optional) - edit `roles/minecraft_server/defaults/main.yml`:
```yaml
minecraft_port: 25565
minecraft_max_players: 20
minecraft_memory_max: 2g
minecraft_difficulty: hard
```

3. **Run playbook**:
```bash
ansible-playbook playbook.yml
```

## Configuration

Edit `roles/minecraft_server/defaults/main.yml` to customize:
- Server settings (port, max players, difficulty, gamemode)
- Memory allocation (`minecraft_memory_max`, `minecraft_memory_min`)
- Java options (`minecraft_java_opts`)
- Data directory (`minecraft_data_dir`)

## Usage

```bash
# Test connection
ansible all -i inventory/hosts.yml -m ping

# Run playbook
ansible-playbook playbook.yml

# Run with tags
ansible-playbook playbook.yml --tags config,container

# Check mode
ansible-playbook playbook.yml --check

# Stop container
ansible all -i inventory/hosts.yml -m shell -a "docker stop minecraft-server" -b

```