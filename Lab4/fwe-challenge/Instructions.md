# FWE-Challenge - Multi-Layer Firewall Evasion 

## Objective

A target machine is protected by a multi-layered firewall. Standard scans reveal only a fraction of what's running. Your mission is to enumerate the target thoroughly, uncover what the firewall is hiding, and find a way to retrieve the flag from a protected service.

This challenge requires **web enumeration**, **advanced Nmap techniques**, and **packet crafting** to bypass multiple layers of defense.

**Flag format:** `ENPM634{...}`

**Difficulty:** Advanced

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
cd Labs/Lab4/fwe-challenge
```

### 3. Start the Lab

```bash
# Pull the image and start the lab
docker compose up -d

# Verify the container is running
docker compose ps
```

### 4. Tear Down

When you are done:
```bash
docker compose down
```

---

## Your Mission

Enumerate the target, understand what's protecting it, and capture the flag. That's it. How you get there is up to you.

---


## Hints

If you're stuck, reach out to your TA or Instructor. They'll point you in the right direction.

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Container won't start | Check logs: `docker compose logs`. Re-pull and restart: `docker compose pull && docker compose up -d --force-recreate` |
| Can't find the target IP | Verify the container is running with `docker compose ps`, then use `docker inspect FWE-Challenge --format '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}'` |


---

## Deliverables

Submit a write-up that includes:

1. The flag
2. All commands you used and their output (scans, web enumeration, final connection)
3. A step-by-step explanation of how you identified each layer of defense and how you bypassed it
4. What each firewall layer was doing and why your bypass technique worked
