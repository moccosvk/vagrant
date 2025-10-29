# k3s Lab on Vagrant + VirtualBox (3 Nodes)

This repo provisions a **3-node** k3s-ready lab on **VirtualBox** using **Vagrant**:
- **Bridged (public) NIC** with **static LAN IPs** (`192.168.0.101–103`)
- **Host-only NIC** for management (`192.168.230.10–12`)
- Optional provision step flips `/bin/sh` → `/bin/bash`

> Base box: `generic/ubuntu2204`

---

## Prerequisites
- VirtualBox 6/7
- Vagrant 2.4+
- A LAN in `192.168.0.0/24` (adjust if different)
- A VirtualBox **Host-only** network on `192.168.230.0/24` (DHCP off)

Create host-only in VirtualBox: **Tools → Network → Host-only Networks → Create**, set:
- IPv4 Address `192.168.230.1`, Mask `255.255.255.0`, DHCP **disabled**.  
Copy its exact name (e.g., `VirtualBox Host-Only Ethernet Adapter #2`).

---

## Files
- `Vagrantfile` – defines 3 VMs: `k3s-master`, `k3s-worker-1`, `k3s-worker-2`.

Key variables inside:
```ruby
public_ips  = ["192.168.0.101","192.168.0.102","192.168.0.103"] # LAN (bridged)
private_ips = ["192.168.230.10","192.168.230.11","192.168.230.12"] # host-only
bridge_name = "Intel(R) Ethernet Connection (17) I219-LM"          # your host NIC
hostonly    = "VirtualBox Host-Only Ethernet Adapter #2"           # from VBox

Quick start

# 1) Clone
git clone https://github.com/moccosvk/vagrant.git
cd <your-dir>/<win or lin>

# 2) Bring up the lab
vagrant up

# 3) SSH into nodes
vagrant ssh k3s-master
vagrant ssh k3s-worker-1
vagrant ssh k3s-worker-2
