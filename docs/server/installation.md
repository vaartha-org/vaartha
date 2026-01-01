# Server Installation Guide

This guide details how to set up the **VAARTHA Registrar** (Server) on a dedicated device (Level 1 & Level 2 Scale).
*For "Host Mode" (running server on your PC/Phone), see the Endpoint Documentation.*

## Prerequisites
*   **Hardware**: Raspberry Pi 4 (4GB RAM) OR Any x86 Laptop/Server.
*   **OS**: Ubuntu 22.04 LTS or Debian 12 (Bookworm).
*   **Network**: Static IP configured on the router (recommended) or use hostname.

## Method A: Docker Compose (Recommended)

### 1. Install Docker
```bash
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER
```

### 2. Clone Repository
```bash
git clone https://github.com/vaartha-org/vaartha-server.git
cd vaartha-server
```

### 3. Configure Env
Edit the `.env` file to set your local domain (default is `vaartha.local`):
```bash
DOMAIN=vaartha.local
TLS_ENABLED=true
```

### 4. Run
```bash
docker compose up -d
```

### 5. Verify
Check if the SIP port is open:
```bash
netstat -ulnp | grep 5060
```

## Method B: Bare Metal (Advanced)

### 1. Install Flexisip
On Debian/Ubuntu:
```bash
sudo apt install flexisip
```

### 2. Configure Flexisip
Edit `/etc/flexisip/flexisip.conf`:
*   Set `transports=sip:0.0.0.0:5060;transport=udp`
*   Set `cluster/enabled=false` (For single node)

### 3. Enable Service
```bash
sudo systemctl enable flexisip
sudo systemctl start flexisip
```

## Troubleshooting
*   **"User not found"**: Check if the client is registering with the correct domain (`@vaartha.local`).
*   **"One-way Audio"**: This is usually a Firewall/NAT issue. Ensure UDP ports 10000-20000 are allowed through the firewall.
