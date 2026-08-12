---
layout: default
title: "Pihole-WireGuard"
---

# Project Implementation: Secure Remote Gateway & DNS Sinkhole

This project details the architectural deployment of an isolated homelab remote gateway and centralized DNS sinkhole. It provides a secure, encrypted tunnel to connect to my local lab network from public environments while enforcing network-wide ad-blocking and DNS auditing.

## Global Setup References
To maintain documentation modularity, the foundational installation steps are drawn from my global wiki repository:
* [General Proxmox LXC Setup Guide](../../raw-steps/lxc-setup.html)
* [General Pi-hole Installation Guide](../../raw-steps/pihole-setup.html)
* [General WireGuard Installation Guide](../../raw-steps/wireguard-setup.html)

## Project-Specific Modifications & Hypervisor Tweaks

### 1. WireGuard LXC Nesting & Kernel Hooking
Because the WireGuard VPN container needs to spin up a virtual network tunnel interface natively, standard LXC restrictions must be bypassed on the Proxmox host shell:
1. In the Proxmox GUI, select the WireGuard container, go to **Options**, and ensure **Nesting** is enabled.
2. Open the primary Proxmox host shell and open the container configuration file:
   ```bash
   nano /etc/pve/lxc/YOUR_CONTAINER_ID.conf
   ```
3. Append these low-level device flags to the bottom of the file to allow TUN device access:
   ```text
   lxc.cgroup2.devices.allow: c 10:200 rwm
   lxc.mount.entry: /dev/net/tun dev/net/tun none bind,create=file
   ```
4. Reboot the container via the host terminal: `pct reboot YOUR_CONTAINER_ID`.

### 2. Edge Router Port Forwarding
To allow inbound external handshakes to reach the WireGuard server LXC container:
* Log into the primary network edge router and forward **UDP Port 51820** directly to the static internal IPv4 address assigned to the WireGuard LXC.

## Infrastructure Verification
Log into the WireGuard container and run `wg show` to verify active connection timers and real-time data handshakes.

[← Back to Projects](./)