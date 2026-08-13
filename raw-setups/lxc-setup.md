---
layout: default
title: "Proxmox LXC Setup"
---

# Linux Container (LXC) Deployment on Proxmox

## Template Downloading
* Select the Proxmox node under **Datacenter** -> select the **local (proxmox)** storage node.
* Click the **CT Templates** tab in the center pane, then click the **Templates** button.
* Search for the desired Ubuntu template (e.g., Ubuntu-24.02) and click **Download**.

## Container Provisioning
* Click **Create CT** in the top right.
* **General:** Set a hostname and password.
* **Template:** Select the downloaded Ubuntu template.
* **Disks:** Set storage to default and adjust disk size to 4–8 GiB.
* **CPU & Memory:** Leave as default (1 core, 512 MiB).
* **Network:** Set IPv4 to **Static**.
* **DNS:** Input preferred upstream DNS servers (e.g., Cloudflare `1.1.1.1` or Google `8.8.8.8`).

## Static IP Logic
* Use the first three octets of your main gateway IP (e.g., `10.50.1.1` becomes `10.50.1.x`).
* Choose an unused 4th digit outside or before your DHCP pool (e.g., `.50` or `.210`). Verify it is open by pinging it first.
* Set the appropriate CIDR suffix based on the subnet mask (`/24` for `255.255.255.0` or `/16` for `255.255.0.0`).
* For Gateway (IPv4), use your default gateway IP.

## SSH Configuration
1. Log into the LXC and edit the configuration: `nano /etc/ssh/sshd_config`.
2. Locate `#PermitRootLogin prohibit-password`, remove the `#`, and change the value to `yes`.
3. Save (`Ctrl + O` -> `Enter` -> `Ctrl + X`) and restart the service: `systemctl restart ssh`.
4. Install OpenSSH server if missing: `apt update && apt install -y openssh-server`.

[← Back to Raw Setups Index](https://rishibambhrolia.github.io/homelab/raw-setups/)