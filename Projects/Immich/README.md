# Immich - Self Hosted Photo Server

## What it is
Immich is a self hosted photo and video backup solution — a private alternative to Google Photos or iCloud. All photos are stored on your own server with no third party access.

---

## Why I built it
- **Family was constantly running out of storage on their phones** due 
  to large photo and video collections with no backup solution
- Needed a way to automatically back up family photos without relying 
  on paid cloud storage like iCloud or Google Photos
- Learn Docker containerization in a real world project
- Set up a self hosted service on Debian Linux
- Give family members a private and unlimited photo backup solution
- Practice server administration and storage management

---

## Hardware
| Component | Details |
|-----------|---------|
| **Server** | Asus X551M running Debian 13 |
| **RAM** | 4GB |
| **Storage** | 500GB SATA HDD |

---

## Tech Stack
| Technology | Purpose |
|-----------|---------|
| **Docker** | Container runtime |
| **Docker Compose** | Multi container management |
| **Immich** | Photo server application |
| **PostgreSQL** | Database (runs in Docker) |
| **Redis** | Cache (runs in Docker) |
| **Debian 13** | Host operating system |

---

## Installation

### Prerequisites
- Debian 13 server with Docker installed
- At least 4GB RAM
- Sufficient storage for photos

### Step 1 — Create directories
```bash
sudo mkdir -p /opt/immich
sudo chown -R $USER:$USER /opt/immich
mkdir -p /home/brian/immich/photos
mkdir -p /home/brian/immich/database
```

### Step 2 — Download Immich files
```bash
cd /opt/immich
wget -O docker-compose.yml https://github.com/immich-app/immich/releases/latest/download/docker-compose.yml
wget -O .env https://github.com/immich-app/immich/releases/latest/download/example.env
```

### Step 3 — Configure environment
```bash
nano /opt/immich/.env
```
Set these values:
```
UPLOAD_LOCATION=/home/brian/immich/photos
DB_DATA_LOCATION=/home/brian/immich/database
DB_PASSWORD=your_secure_password
```

### Step 4 — Start Immich
```bash
cd /opt/immich
sudo docker compose up -d
```

### Step 5 — Verify running
```bash
sudo docker compose ps
```

---

## Accessing Immich
Open a browser on any device on your home network:
```
http://YOUR-SERVER-IP:2283
```

Find your server IP with:
```bash
hostname -I
```

---

## Mobile App Setup
1. Download **Immich** from App Store or Google Play
2. Enter server URL: `http://YOUR-SERVER-IP:2283`
3. Log in with your credentials
4. Enable **Auto Backup** in app settings
5. Set WiFi only backup to save mobile data

---

## Storage Layout
```
/opt/immich/
├── docker-compose.yml
└── .env

/home/brian/immich/
├── photos/
│   ├── upload/       ← actual photos and videos
│   ├── thumbs/       ← auto generated thumbnails
│   ├── encoded-video/← transcoded videos
│   ├── backups/      ← database backups
│   └── profile/      ← user profile pictures
└── database/         ← PostgreSQL data
```

---

## Backup Strategy
| Backup | What | When |
|--------|------|------|
| **Database** | Metadata, albums, faces | Automatic daily 2AM |
| **Photos** | Actual photo files | Manual to external drive |

---

## Problems I Solved
- **Permission denied creating /opt/immich** — fixed with `sudo chown`
- **YAML constructor error** — fixed by redownloading docker-compose.yml with wget
- **curl permission denied** — fixed by correcting folder ownership
- **Immich machine learning slow** — expected on Celeron CPU, runs in background

---

## Useful Commands
```bash
# Start Immich
cd /opt/immich && sudo docker compose up -d

# Stop Immich
cd /opt/immich && sudo docker compose down

# Check status
sudo docker compose ps

# View logs
sudo docker compose logs -f

# Check storage usage
df -h
du -sh /home/brian/immich/photos/
```

---

## What I Learned
- Docker Compose multi container application deployment
- Managing persistent storage with Docker volumes
- Linux file permissions and ownership
- Self hosted service administration
- Storage planning and management
