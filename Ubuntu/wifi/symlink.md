### 1️⃣ Check where it points

`ls -l /etc/resolv.conf`

Example output:

`lrwxrwxrwx 1 root root 39 Nov 10 20:00 /etc/resolv.conf -> ../run/systemd/resolve/stub-resolv.conf`

- This shows it points to the `systemd-resolved` stub.
    

---

### 2️⃣ If you want to keep `systemd-resolved` (recommended)

- Make sure the service is running:
    

`systemctl status systemd-resolved`

- Check the current DNS servers:
    

`resolvectl status`

- This setup is fine; you **don’t need to edit `/etc/resolv.conf` manually**.
    

---

### 3️⃣ If you want to replace it with a static resolv.conf

1. Remove the symlink:
    

`sudo rm /etc/resolv.conf`

2. Create a new file:
    

`sudo nano /etc/resolv.conf`

3. Add your DNS servers, e.g.:
    

`nameserver 8.8.8.8 nameserver 8.8.4.4`

4. Save and exit.
    

---

### 4️⃣ If DNS is broken but you want `systemd-resolved`

- Sometimes the symlink is missing or wrong:
    

`sudo ln -sf /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf sudo systemctl restart systemd-resolved`

---

💡 **Tip:** Keeping the symlink to `systemd-resolved` is usually best for modern Linux systems, unless you have a specific reason to use a static `resolv.conf`.

I can also give you a **quick command to fix DNS for most Linux distros in one line** if you want. Do you want me to do that?