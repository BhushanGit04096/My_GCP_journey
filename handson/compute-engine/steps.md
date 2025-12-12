# Compute Engine Hands-on Labs

This document contains all required labs for mastering Google Compute Engine.  
Complete each section and upload screenshots inside `screenshots/` folder.

---

## 🟩 1. VM Creation + nginx Lab (Basic)

1. Open Google Cloud Console → Compute Engine → VM instances.
2. Click **Create instance**.
   - Name: `lab-vm-nginx`
   - Region/zone: us-central1 / us-central1-a
   - Machine type: `e2-medium` (or `e2-micro` free tier)
   - Boot disk: Click **Change** → choose **Debian 11 (bullseye)** → Select
   - Under “Firewall” check **Allow HTTP traffic** and **Allow HTTPS traffic**
3. Click **Create** and wait until VM is RUNNING.
4. Note the **External IP** (`vm-created.png`).
5. Click **SSH** (`ssh-connected.png`).
6. Install nginx in VM (see `commands.md`).
7. Verify locally:
   ```bash
   curl http://localhost
   curl -I http://localhost
   ```
8. Verify externally:
   ```
   http://<EXTERNAL_IP>
   ```
   (`site-working.png`)
9. Create snapshot:
   - Compute Engine → Disks → boot disk → Create snapshot  
   - Name `lab-vm-nginx-snap1`  
   (`snapshot-created.png`)
10. Optional: Create image from snapshot (Images → Create image)
11. Cleanup if VM not required.

---

## 🟩 2. Internal vs External IPs Lab

1. Create **two VMs** in same VPC.
2. SSH into VM1:
   ```bash
   ping <VM2_INTERNAL_IP>
   curl http://<VM2_INTERNAL_IP>
   ```
3. Test external:
   ```bash
   curl http://<VM2_EXTERNAL_IP>
   ```
4. Screenshots:
   - `internal-ping.png`
   - `internal-curl.png`
   - `external-failed.png`

---

## 🟩 3. Resize Boot Disk

1. VM instances → Click VM → **Edit**.
2. Boot Disk → **Edit** → increase disk size (10GB → 20GB).
3. SSH:
   ```bash
   df -h
   sudo growpart /dev/sda 1
   sudo resize2fs /dev/sda1
   df -h
   ```
4. Screenshots: `disk-before.png`, `disk-after.png`.

---

## 🟩 4. Attach Additional Disk

1. Compute Engine → Disks → **Create Disk** (10GB).
2. Attach disk to VM.
3. SSH:
   ```bash
   lsblk
   sudo mkfs.ext4 /dev/sdb
   sudo mkdir /data
   sudo mount /dev/sdb /data
   df -h
   ```
4. Add in `/etc/fstab`:
   ```
   /dev/sdb   /data   ext4   defaults   0  2
   ```
5. Screenshots: `disk-attached.png`, `disk-mounted.png`.

---

## 🟩 5. Startup Script (Metadata Automation)

1. VM → **Edit → Management → Metadata**.
2. Key: `startup-script`  
   Value:
   ```bash
   #!/bin/bash
   apt update
   apt install -y nginx
   echo "Deployed via startup script" > /var/www/html/index.html
   ```
3. Reset/recreate VM.
4. Screenshot: `startup-script-working.png`.

---

## 🟩 6. Static External IP

1. VPC Network → External IP addresses.
2. Change Ephemeral → **Reserved**.
3. Stop/start VM → confirm IP unchanged.
4. Screenshot: `static-ip.png`.

---

## 🟩 7. Custom Firewall Rule (Port 8080)

1. VPC Network → Firewall rules → Create rule:
   - Name: `allow-8080`
   - Direction: Ingress
   - Source: `0.0.0.0/0`
   - Protocols/Ports: TCP:8080
2. SSH:
   ```bash
   echo "Hello from port 8080" | sudo nc -l -p 8080
   ```
3. Browser:
   ```
   http://<EXTERNAL_IP>:8080
   ```
4. Screenshot: `port8080-working.png`.

---

## 🟩 8. Windows VM + RDP

1. Create **Windows Server** VM.
2. VM → **Set Windows password**.
3. Download RDP file and connect.
4. Screenshot: `windows-rdp.png`.

---

## 🟩 9. Service Accounts + IAM Scopes

1. Create VM with **No Access** to Storage.
2. SSH:
   ```bash
   gsutil ls
   ```
   → should fail (`sa-fail.png`).
3. Grant service account **Storage Viewer**.
4. SSH again:
   ```bash
   gsutil ls
   ```
   → should work (`sa-success.png`).

---

## 🟩 10. Metadata Server Basics

Run inside VM:
```bash
curl -H "Metadata-Flavor: Google" \
"http://metadata.google.internal/computeMetadata/v1/"
```
Screenshot: `metadata-server.png`.

---

## 🟩 11. Create Custom Image from Snapshot

1. Compute Engine → Images → Create Image.
2. Source: your snapshot.
3. Create a VM using this custom image.
4. Screenshot: `custom-image-vm.png`.

---

## 📁 Recommended Folder Structure

```
handson/
  compute-engine/
    README.md
    commands.md
    screenshots/
    snapshots/
    startup-scripts/
```

---

## ✔ Completion

Finishing all these labs makes you fully ready for GCP Associate Cloud Engineer and real production Compute Engine tasks.
