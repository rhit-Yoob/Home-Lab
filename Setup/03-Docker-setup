# Docker Installation on Debian

## Overview
Docker is a containerization platform that lets you run applications in isolated containers. Essential for DevOps and cloud engineering.

---

## Why Docker
- Run applications without installing dependencies directly on the server
- Easy to deploy, update, and remove services
- Industry standard for DevOps and cloud engineering
- Powers projects like Immich, Pi-hole, Portainer and more

---

## Step 1 — Update System
Always update before installing new software:
```bash
sudo apt update && sudo apt upgrade -y
```

---

## Step 2 — Install curl
```bash
sudo apt install curl -y
```

---

## Step 3 — Download Docker Install Script
```bash
curl -fsSL https://get.docker.com -o get-docker.sh
```

---

## Step 4 — Run Docker Install Script
```bash
sudo sh get-docker.sh
```
This automatically installs the latest version of Docker for your OS.

---

## Step 5 — Add User to Docker Group
Replace `brian` with your username — this lets you run Docker without sudo every time:
```bash
sudo usermod -aG docker brian
```

---

## Step 6 — Enable and Start Docker
```bash
sudo systemctl enable docker
sudo systemctl start docker
```

---

## Step 7 — Log Out and Back In
```bash
logout
```
Log back in to apply the Docker group membership.

---

## Step 8 — Verify Docker is Working
Check Docker version:
```bash
docker --version
```

Run test container:
```bash
docker run hello-world
```
You should see **Hello from Docker!** — Docker is working! ✅

---

## Step 9 — Install Docker Compose Plugin
```bash
sudo apt install docker-compose-plugin -y
```

Verify:
```bash
docker compose version
```

---

## Useful Docker Commands
```bash
# List running containers
docker ps

# List all containers including stopped
docker ps -a

# List downloaded images
docker images

# Stop a container
docker stop container_name

# Remove a container
docker rm container_name

# View container logs
docker logs container_name

# Check Docker disk usage
docker system df

# Remove unused images and containers
docker system prune
```

---

## Docker Compose Commands
```bash
# Start services in background
docker compose up -d

# Stop services
docker compose down

# View running services
docker compose ps

# View logs
docker compose logs -f

# Restart services
docker compose restart
```

---

## What I Learned
- Docker container lifecycle management
- Running multi container applications with Docker Compose
- Managing Docker images and volumes
- Linux service management with systemctl
