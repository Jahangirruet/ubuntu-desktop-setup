# Ubuntu Server Setup Guide

## 1. Download Ubuntu Desktop ISO

Download the Ubuntu Desktop ISO from the official Ubuntu website:

🔗 [Ubuntu Download](https://ubuntu.com/download)

> The ISO file may download slowly as the server is located in a nearby local country. This method is recommended for installing Linux on a local machine (e.g., using VirtualBox).

For Proxmox installations, use the alternative download link:

🔗 [Alternative Ubuntu Download](https://launchpad.net/ubuntu/+cdmirrors)

---

## 2. Retrieve MAC Address

Ensure you keep the MAC address from the IP list for reference.

---

## 3. Follow Windows Setup Steps

The rest of the process is similar to the Windows setup.

---

## 4. Make the Server SSH Accessible

### Check Internet Connection

Run the following commands to verify connectivity:

```bash
ping google.com
```

or

```bash
ping 8.8.8.8
```

Alternatively, open a browser and try visiting any website.

### Install OpenSSH Server

```bash
sudo apt update
sudo apt install openssh-server -y
```

### Verify SSH Service Status

```bash
sudo systemctl status ssh
```

If SSH is inactive, start it:

```bash
sudo systemctl start ssh
```

Enable SSH to start on boot:

```bash
sudo systemctl enable ssh
```

### Allow SSH Through Firewall (if applicable)

```bash
sudo ufw allow ssh
sudo ufw enable  # Enable firewall if not already enabled
sudo ufw status  # Check firewall rules
```

### Check SSH Connection

```bash
ssh username@your_server_ip
```

#### Issue: Remote Host Identification Has Changed

```bash
ssh ubuntu@51.81.20.84
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
...
Host key verification failed
```

#### Solution:

```bash
ssh-keygen -R 51.81.20.84
```

---

## 5. Enable Remote Desktop (RDP) in Ubuntu

Ubuntu 24.04 supports **GNOME Remote Desktop (based on RDP)** by default.

### Step 1: Open Remote Desktop Settings
1. Open "Settings" from the system menu.
2. Navigate to "Sharing".
3. Enable **"Remote Desktop"**.

### Step 2: Configure Access
- Turn on **"Remote Desktop"**.
- Enable **"Remote Control"**.
- Set a **Username & Password** for authentication.
- (Optional) Enable **"Require password for connections"**.

### Step 3: Allow RDP Through Firewall

Ubuntu's firewall (UFW) may block RDP connections. Run the following:

```bash
sudo ufw allow 3389/tcp
sudo ufw enable
```

Check the firewall status:

```bash
sudo ufw status
```

