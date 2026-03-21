# n8n Docker Setup

## Prerequisites

- Docker installed

## Setup

### 1. Fix Docker permissions (one-time)

```bash
sudo usermod -aG docker $USER
newgrp docker
```

### 2. Run n8n

```bash
docker run -d --name n8n --restart unless-stopped -p 5678:5678 \
    -v n8n_data:/home/node/.n8n \
    docker.n8n.io/n8nio/n8n
```

n8n will be available at **http://localhost:5678**

## Useful Commands

```bash
# Check running containers
docker ps

# Check all containers (including stopped)
docker ps -a

# Start
docker start n8n

# Stop
docker stop n8n

# Restart
docker restart n8n

# View logs
docker logs -f n8n

# Inspect container details (IP, mounts, env vars, etc.)
docker inspect n8n

# Check resource usage (CPU, memory)
docker stats n8n

# Open a shell inside the container
docker exec -it n8n sh

# Remove container (data is preserved in the volume)
docker rm -f n8n

# List volumes
docker volume ls

# Remove the data volume (WARNING: deletes all n8n data)
docker volume rm n8n_data
```
