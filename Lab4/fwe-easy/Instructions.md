# FWE-Easy - Firewall Evasion Challenge

## Objective

A target machine is running behind a firewall. Some services are accessible, others appear blocked. Your goal is to figure out what the firewall is doing, find a way past it, and retrieve the flag hidden in a service banner.

**Flag format:** `ENPM634{...}`

---

## Setting Up the Lab

### 1. Install Docker

If Docker is not already installed on your system:

```bash
# Update package index
sudo apt update

# Install Docker
sudo apt install -y docker.io docker-compose-v2

# Add your user to the docker group (avoids needing sudo for docker commands)
sudo usermod -aG docker $USER

# Log out and back in for the group change to take effect, or run:
newgrp docker

# Verify installation
docker --version
docker compose version
```

### 2. Clone the Repository

```bash
git clone https://github.com/ENPM634Corp/Labs.git
cd Labs/Lab4/fwe-easy
```

### 3. Start the Lab

```bash
# Pull and start the lab
docker compose up -d fwe-easy

# Verify the container is running
docker compose ps

# Find the target IP
docker inspect FWE-Easy --format '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}'
```

### 4. Tear Down

When you are done:
```bash
docker compose down
```

---

## Your Mission

The target machine is running three services: **FTP (21)**, **SSH (22)**, and **HTTP (80)**. A firewall sits in front of them.

1. Run a standard scan against the target. Observe which ports are open and which are not directly accessible.

2. Investigate the firewall. Determine what kind of filtering is in place and whether it has any weaknesses in how it inspects traffic.

3. Find a way to reach the blocked service and extract its banner. The flag is in the banner.

---

## Hint

> Not all scan types interact with firewalls the same way. If one type of probe is being blocked, think about what makes that probe different from others at the TCP level and whether the firewall is smart enough to tell the difference.

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| All ports show `filtered` | Make sure you're scanning the container IP, not localhost. Verify the container is running with `docker compose ps` |
| Container won't start | Check logs: `docker compose logs fwe-easy`. Recreate: `docker compose up -d --force-recreate fwe-easy` |
| `Pool overlaps with other one on this address space` | Another Docker network is using the same subnet. Run `docker network prune` to remove unused networks, then try again. If it still fails, stop any other running containers first with `docker compose down` in their respective directories |
| A tool complains a port is already in use | Another process may be occupying that port. Identify it with `sudo lsof -i :<port>` and stop it if needed |

---

## Deliverables

Submit a short write-up that includes:

1. The flag
2. The Nmap commands you used and their output
3. A brief explanation of why your approach worked
