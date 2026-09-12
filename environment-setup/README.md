# 🧪 Cybersecurity Lab Environment Setup

This directory documents the initial laboratory environment created for the Networkwalks Cybersecurity Internship.

## Objective

The objective of this setup was to create a controlled cybersecurity environment using Kali Linux and Oracle VirtualBox.

## Lab Configuration

```text
Host OS       : Windows
Hypervisor    : Oracle VirtualBox
Guest OS      : Kali Linux
Network       : NetworkWalksNAT
Network CIDR  : 10.10.10.0/24
DHCP          : Enabled
```

## Setup Workflow

```text
Create NAT Network
        ↓
Configure Kali Linux
        ↓
Connect Kali to NAT Network
        ↓
Create Initial Snapshot
        ↓
Verify IP Configuration
        ↓
Test Network Connectivity
        ↓
Configure Shared Folder
        ↓
Begin Security Labs
```

## Evidence

| #  | Activity                    | Evidence                                                 |
| -- | --------------------------- | -------------------------------------------------------- |
| 01 | NAT Network Creation        | [View](screenshots/01-create-nat-network.png)            |
| 02 | Kali Network Configuration  | [View](screenshots/02-kali-connected-to-nat-network.png) |
| 03 | Initial Snapshot            | [View](screenshots/03-first-snapshot.png)                |
| 04 | IP Address Verification     | [View](screenshots/04-kali-ip-address.png)               |
| 05 | Connectivity Verification   | [View](screenshots/05-network-connectivity.png)          |
| 06 | Shared Folder Configuration | [View](screenshots/06-shared-folder.png)                 |

## Verification Commands

### Check interfaces

```bash
ifconfig
```

### Check IP addressing

```bash
ip addr
```

### Check routing

```bash
ip route
```

### Test connectivity

```bash
ping -c 4 8.8.8.8
```

## Result

The initial cybersecurity laboratory environment was successfully configured and verified, providing a controlled platform for subsequent cybersecurity exercises.
