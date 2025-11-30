# 🧠 DNS / resolv.conf Management Cheat Sheet (Linux)

## 🧩 1. Check where `/etc/resolv.conf` points
```bash
ls -l /etc/resolv.conf 
```
- Shows if it’s a symlink (e.g., → `../run/systemd/resolve/stub-resolv.conf`).
## 🧩 2. Edit `/etc/resolv.conf` manually (temporary)
```
sudo nano /etc/resolv.conf

```
- ⚠️ If `systemd-resolved` manages it, your changes will be **overwritten** automatically.
## ## 🧩 3. View DNS status and current servers

`resolvectl status`

> Shows which DNS servers and domains are active per interface.

## 🧩 5. Restart DNS resolver service

`sudo systemctl restart systemd-resolved`

---

## 🧩 6. Flush DNS cache

`sudo resolvectl flush-caches`

---

## 🧩 7. Check logs related to DNS resolution

`journalctl -u systemd-resolved --since "10 minutes ago"`

---

## 🧩 8. Set custom DNS servers temporarily (example: Cloudflare)

`sudo resolvectl dns wlp4s0 1.1.1.1 1.0.0.1`

> Replace `wlp4s0` with your network interface name (use `ip link` to list).

---

## 🧩 9. Make `/etc/resolv.conf` static (optional)

`sudo rm /etc/resolv.conf echo -e "nameserver 1.1.1.1\nnameserver 1.0.0.1" | sudo tee /etc/resolv.conf`

> ⚠️ This disables systemd’s automatic DNS management — useful only if you want full manual control.

---

## 🧩 10. Check network interfaces

`ip link`

---

## 🧩 11. Verify active connection and DNS

`nmcli dev show | grep DNS`

> Displays DNS info managed by NetworkManager.

---

## 🧩 12. Reload DHCP client (if using dhcpcd)

`sudo systemctl restart dhcpcd`

---

✅ **Quick summary**

- `/etc/resolv.conf` is usually a symlink to a systemd-managed file.
    
- Use `resolvectl` for DNS diagnostics and manual DNS changes.
    
- Manual edits get replaced unless you disable `systemd-resolved`.
    
- Cloudflare WARP or VPNs may dynamically set DNS servers.