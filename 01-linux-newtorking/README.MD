# 🖥️ Project 01: Remote Linux Server Setup (SSH) & LAN Troubleshooting

## 📖 Overview
As part of my journey towards Cloud Infrastructure and DevOps, this mini-project demonstrates the configuration of secure remote access (SSH) to a physical Linux server from a Windows client. It also documents a real-world Local Area Network (LAN) troubleshooting scenario involving VPN tunneling.

## 🏗️ Architecture
* **Client:** Windows 10 (Native OpenSSH Client)
* **Server:** Ubuntu Linux (OpenSSH Server)
* **Protocol:** SSH (Port 22)
* **Network:** Local Area Network (Wi-Fi)

## 🐛 Troubleshooting: The "General Failure" Issue
**Problem:** During the initial network validation, pinging the Linux server from the Windows client resulted in a `General failure` (instead of a typical `Request timed out`).

**Root Cause:** An active VPN client on the Windows machine was forcibly routing all traffic through its encrypted tunnel, overriding local subnet routes and dropping local ICMP packets to the `192.168.1.107` network.

**Solution:** Enabled "Split Tunneling" in the VPN settings, allowing traffic to bypass the VPN tunnel and reach the local subnet directly.

## ⚙️ Server Configuration Steps
Executed on the target Linux machine to enable secure remote access:

1. **Update package lists & install SSH daemon:**
   ```
   sudo apt update
   sudo apt install openssh-server -y
  ```

2. **Start and verify the SSH service**
  ```
  sudo systemctl start ssh
  sudo systemctl status ssh
  ```

3. **Allow SSH traffic through firewall: (It worked overall, but I did it just in case.)**
  ```
  sudo ufw allow ssh
  ```

🔑 **Client Connection**
Connected successfully from the Windows terminal to estabilish the client-server architecture:
  ```
  ssh ajgorek@192.168.1.107
  ```
###### Accepted the ED25519 key fingerprint (Trust on First Use mechanism) to establish the secure connection.
