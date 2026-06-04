# Home Lab - Debian Linux Server

## Overview
Personal home lab server built on Debian 13 Linux. Built to develop real world skills in DevOps, SysAdmin, and Cloud Engineering in preparation for industry certifications.

---

## Hardware
| Component | Details |
|-----------|---------|
| **Laptop** | Asus X551M |
| **CPU** | Intel Celeron dual core 1.8GHz |
| **RAM** | 4GB |
| **Storage** | 500GB SATA HDD |
| **OS** | Debian 13 Bookworm |

---

## Challenges & Problem Solving
Real hardware and software issues encountered and resolved during setup:

- Diagnosed a **failing NVMe SSD** on HP Pavilion x360 using `dmesg` and identified bad sectors via buffer IO errors
- Resolved **corrupted USB drives** causing IO errors during OS flashing
- Fixed **UEFI Secure Boot** issues blocking Linux installation on HP hardware
- Cleared **corrupted Windows hibernation data** blocking partition formatting using `ntfsfix`
- Manually **partitioned disk** using command line tools when GUI installer failed
- Resolved **Intel RST/RAID** conflicts preventing Ubuntu from detecting NVMe drive
- Troubleshot **network boot issues** and configured BIOS boot order on multiple laptops
- Added user to **sudoers** and configured sudo access on Debian
- Configured **lid close behavior** to keep server running when laptop is closed

---

## Setup
Step by step guides for rebuilding this server from scratch:

1. [Debian Install](Setup/01-Debian-Install.md)
2. [Sudo and User Setup](Setup/02-Sudo&User-Setup.md)
3. [Docker Installation](Setup/03-Docker-Setup.md)

---

## Projects
| Project | Description | Status |
|---------|-------------|--------|
| [Immich](Projects/Immich/README.md) | Self hosted photo and video backup server | ✅ Complete |

---

## Scripts
Automation scripts for server management:

---

## Skills Demonstrated
- Linux installation and system administration
- BIOS/UEFI configuration and troubleshooting
- Disk partitioning and storage management
- Hardware diagnostics and problem solving
- SSH server configuration
- Docker containerization
- Bash scripting
- Git version control
- Technical documentation

---

## Connect
- **GitHub:** [github.com/rhit-Yoob](https://github.com/rhit-Yoob)
- **LinkedIn:** [linkedin.com/in/brian-yoo-422a2b288](https://www.linkedin.com/in/brian-yoo-422a2b288)
