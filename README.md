# Qubes OS LAN-only Firewall Playbook

This Ansible playbook creates a dedicated **LAN-only firewall qube** inside a Qubes OS environment.  
It is designed for users who want to isolate local network access (e.g., NAS, printers, or intranet hosts) from the Internet while maintaining internal connectivity between trusted domains.

---

## Overview

The playbook performs the following actions:

1. **Creates a new Qube** named `sys-lan-firewall`, based on a chosen template (e.g. `debian-13`).
2. Configures it to **provide a network** (acts as a NetVM).
3. Deploys a **custom nftables configuration** that:
   - Allows traffic only within private LAN address ranges (IPv4 and IPv6 local scopes).
   - Blocks all Internet-bound traffic.
4. Ensures the custom firewall rules are **persisted** across reboots via `/rw/config/rc.local`.
5. Applies the nftables rules **immediately without reboot**.

---

## Requirements

- **Qubes OS** (tested on R4.3)
- **qubes-ansible** module installed in `dom0`
- **nftables** available in the firewall template qube (install with `sudo apt install nftables` or `sudo dnf install nftables` if missing)

---

## Usage

Run the playbook:

```bash
ansible-playbook createVM-sys-lan-firewall.yml
