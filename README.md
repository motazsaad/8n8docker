# AI Agent Tools Docker Setup

## Prerequisites

- Docker installed

## Setup

### 1. Fix Docker permissions (one-time)

```bash
sudo usermod -aG docker $USER
newgrp docker
```

### 2. Run n8n on a workstation 

```bash
docker run -d --name n8n --restart unless-stopped \
    -p 0.0.0.0:5678:5678 \
    -e N8N_LISTEN_ADDRESS=0.0.0.0 \
    -e N8N_SECURE_COOKIE=false \
    -v n8n_data:/home/node/.n8n \
    docker.n8n.io/n8nio/n8n
```
## Run n8n on locally 
```bash
docker run -d --name n8n --restart unless-stopped \
    -p 5678:5678 \
    -v n8n_data:/home/node/.n8n \
    docker.n8n.io/n8nio/n8n
```

n8n will be available at **http://localhost:5678**

### 3. Run Flowise AI on a workstation

```bash
docker run -d --name flowise --restart unless-stopped \
    -p 0.0.0.0:3000:3000 \
    -v flowise_data:/root/.flowise \
    flowiseai/flowise:latest
```

## Run Flowise AI locally

```bash
docker run -d --name flowise --restart unless-stopped \
    -p 3000:3000 \
    -v flowise_data:/root/.flowise \
    flowiseai/flowise:latest
```

Flowise AI will be available at **http://localhost:3000**

## Useful Commands

```bash
# Check running containers
docker ps

# Check all containers (including stopped)
docker ps -a

# Start/Stop n8n
docker start n8n
docker stop n8n

# Restart n8n
docker restart n8n

# Start/Stop Flowise AI
docker start flowise
docker stop flowise

# Restart Flowise AI
docker restart flowise

# View logs
docker logs -f n8n
docker logs -f flowise

# Inspect container details (IP, mounts, env vars, etc.)
docker inspect n8n
docker inspect flowise

# Check resource usage (CPU, memory)
docker stats n8n flowise

# Open a shell inside the container
docker exec -it n8n sh
docker exec -it flowise sh

# Remove container (data is preserved in the volume)
docker rm -f n8n
docker rm -f flowise

# List volumes
docker volume ls

# Remove the data volumes (WARNING: deletes all data)
docker volume rm n8n_data
docker volume rm flowise_data
```
