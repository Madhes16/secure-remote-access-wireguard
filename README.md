# secure-remote-access-wireguard
Implemented a secure remote access solution using WireGuard VPN on Ubuntu Linux. Configured encrypted tunnels, firewall rules, and IP forwarding to allow safe communication between remote clients and a private server. Documented installation steps, troubleshooting, and testing procedures for reliable remote connectivity.

# WireGuard VPN Setup Project

## 📌 Project Overview
This project demonstrates how to set up a secure VPN tunnel using WireGuard to remotely access a private Linux server.

The VPN allows secure communication between:
- Remote Client (Laptop)
- Private Server (Ubuntu)

## 🧰 Technologies Used
- WireGuard VPN
- Ubuntu Server
- Linux Networking
- UFW Firewall
- SSH

## 🖥️ Lab Setup

Server:
- OS: Ubuntu 22.04
- Public IP: XXX.XXX.XXX.XXX (masked)
- VPN Network: 10.0.0.0/24

Client:
- OS: Windows 10 / Linux
- WireGuard Client Installed

## 🔧 Installation Steps

### Step 1 — Install WireGuard

```bash
sudo apt update
sudo apt install wireguard -y
```

### Step 2 — Generate Keys

```bash
wg genkey | tee privatekey | wg pubkey > publickey
```

### Step 3 — Configure Server

Example `/etc/wireguard/wg0.conf`

```ini
[Interface]
Address = 10.0.0.1/24
ListenPort = 51820
PrivateKey = SERVER_PRIVATE_KEY

[Peer]
PublicKey = CLIENT_PUBLIC_KEY
AllowedIPs = 10.0.0.2/32
```

### Step 4 — Enable IP Forwarding

```bash
sudo nano /etc/sysctl.conf
net.ipv4.ip_forward=1
```

### Step 5 — Start WireGuard

```bash
sudo wg-quick up wg0
sudo systemctl enable wg-quick@wg0
```

## 🔐 Security Features
- Encrypted VPN Tunnel
- Private Key Authentication
- Firewall Rules using UFW

## 🌐 Network Diagram

This diagram shows the WireGuard VPN tunnel between the remote client and private server.

![WireGuard VPN Diagram](Wireguard%20Diagram.png)

## 🧪 Testing

Verified connection using:

```bash
ping 10.0.0.1
wg show
```

## 📷 Screenshots

(Add screenshots)

## 📚 Learning Outcome

- Learned VPN tunneling concepts
- Implemented secure remote access
- Configured firewall and routing
- Understood public/private key encryption

## 🚀 Future Improvements

- Add multiple clients
- Deploy on AWS EC2
- Add monitoring with Nagios/Zabbix
