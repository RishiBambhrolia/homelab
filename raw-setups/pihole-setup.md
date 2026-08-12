---
layout: default
title: "Pi-hole Setup"
---

# Pi-hole DNS Sinkhole Deployment Guide

## Installation
1. Run system updates and install curl:
   ```bash
   apt update && apt upgrade -y && apt install -y curl
   ```
2. Run the automated Pi-hole installer:
   ```bash
   curl -sSL [https://install.pi-hole.net](https://install.pi-hole.net) | bash
   ```
3. Complete the installation wizard using default options.
4. Set the admin password:
   ```bash
   pihole setpassword YourNewPasswordHere
   ```

## Web UI Optimization
1. Access the web interface via a browser and log in.
2. Toggle the interface setting from **Basic** to **Expert** mode in the top right corner.
3. Navigate to **Settings** -> **DNS** tab.
4. Under Interface Settings, enable **Respond only on interface eth0**. *(Note: This is safe because the Pi-hole is protected within your internal private network gateway, not exposed to the public cloud)*.

[← Back to Raw Setups](./)