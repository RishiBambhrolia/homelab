---
layout: default
title: "WireGuard Setup"
---

# Native WireGuard VPN Gateway Setup

## Service Installation
1. Update packages and pull the installation script:
   ```bash
   apt update && apt upgrade -y && apt install -y curl wget
   wget [https://raw.githubusercontent.com/Nyr/wireguard-install/master/wireguard-install.sh](https://raw.githubusercontent.com/Nyr/wireguard-install/master/wireguard-install.sh) -O wireguard-install.sh
   chmod +x wireguard-install.sh
   ./wireguard-install.sh
   ```
2. Follow the setup prompts. When asked for a DNS server, choose **Custom** and enter your local **Pi-hole LXC IP address** if you are planning to use Pi-hole, if not then pick any DNS of your choosing.

## Client Management
* **Adding Profiles:** Re-run `./wireguard-install.sh` at any time to add new devices.
* **Mobile Devices:** Scan the generated terminal QR code via the WireGuard mobile app. Test functionality by disabling Wi-Fi and checking the active handshake timer (`wg show`).
* **PC Devices:** Use `cat profile_name.conf` to display the config, copy it, and paste it into "Add Empty Tunnel" inside the desktop WireGuard app. Adjust the **AllowedIPs** line to specify your exact home network subnet and VPN pool ranges.

### Here is the link to go back to the Raw Setups page:
* [Browse All General Raw Setups for Future Projects](./raw-setups/README.md)