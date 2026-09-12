# 🧪 Week 01 — Cybersecurity Lab Environment Setup

This directory documents the activities and laboratory setup completed during **Week 01** of the Networkwalks Cybersecurity Internship.

---

## 🎯 Week 01 Objectives

The goal of Week 01 was to establish a secure, controlled, and fully functional cybersecurity laboratory environment using Kali Linux and Oracle VirtualBox, while verifying network configuration, connectivity, baseline snapshots, and host integration.

---

## ⚙️ Lab Configuration Summary

| Component | Specification / Setting |
|---|---|
| **Host OS** | Windows 11 Pro |
| **Hypervisor** | Oracle VirtualBox |
| **Guest OS** | Kali Linux (2026.2) |
| **Network Type** | VirtualBox NAT Network |
| **NAT Network Name** | `NetworkWalksNAT` |
| **Network Subnet (CIDR)** | `10.10.10.0/24` |
| **DHCP Server** | Enabled |
| **Assigned Guest IP** | `10.10.10.3` |
| **Recovery Point** | VirtualBox Snapshot (`First_Snapshots`) |
| **Host-Guest Integration** | VirtualBox Shared Folder (`sf_Downloads`) |

---

## 🔄 Setup Workflow

```text
Create NAT Network (NetworkWalksNAT: 10.10.10.0/24)
                        │
                        ▼
Connect Kali Linux VM to NAT Network
                        │
                        ▼
Create Clean Baseline Snapshot (First_Snapshots)
                        │
                        ▼
Boot Kali Linux & Verify IP Address (10.10.10.3)
                        │
                        ▼
Test Network Connectivity (Browser & Ping)
                        │
                        ▼
Configure VirtualBox Shared Folder (sf_Downloads)
```

---

## 📸 Lab Evidence & Documentation

### 01 — NAT Network Creation
Configured a dedicated VirtualBox NAT Network named `NetworkWalksNAT` with IPv4 CIDR `10.10.10.0/24` and DHCP enabled.

![Create NAT Network](screenshots/01-create-nat-network.png)

---

### 02 — Kali Linux Connected to NAT Network
Attached the Kali Linux virtual machine's network adapter to `NetworkWalksNAT` with promiscuous mode set and virtual cable connected.

![Kali Connected to NAT Network](screenshots/02-kali-connected-to-nat-network.png)

---

### 03 — Baseline VirtualBox Snapshot
Created an initial clean snapshot named `First_Snapshots` prior to starting laboratory exercises, providing an immediate recovery point.

![First Snapshot](screenshots/03-first-snapshot.png)

---

### 04 — Kali Linux IP Address Verification
Booted Kali Linux and executed `ifconfig` in terminal to confirm dynamic IP assignment on `eth0` (`10.10.10.3/24`).

![Kali IP Address](screenshots/04-kali-ip-address.png)

---

### 05 — Network Connectivity Verification
Verified outbound network and Internet connectivity from Kali Linux by successfully browsing web services.

![Network Connectivity](screenshots/05-network-connectivity.png)

---

### 06 — Shared Folder Integration
Configured a VirtualBox Shared Folder (`sf_Downloads`) to allow controlled file exchange between the Windows host system and the Kali Linux guest environment.

![Shared Folder](screenshots/06-shared-folder.png)

---

## 🛠️ Verification Commands Executed

### Interface & IP Address Check
```bash
ifconfig
```
or
```bash
ip addr show eth0
```

### Routing Table Verification
```bash
ip route
```

### ICMP Connectivity Test
```bash
ping -c 4 8.8.8.8
```

---

## 🏁 Week 01 Outcome

The initial cybersecurity laboratory environment was successfully built, isolated, verified, and documented. The environment is now fully ready for subsequent security testing, network analysis, and vulnerability assessment exercises in upcoming weeks.
