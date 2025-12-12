# Compute Engine — Hands-On

**Objective**  
Create and manage Google Compute Engine VMs, install a web server, verify external access, and create recovery artifacts (snapshots/images). Document commands and evidence.

---

## What I built
- A Debian Linux VM (lab-vm-nginx)
- Installed and verified nginx web server
- Created a snapshot of the boot disk for recovery

---

## Topics covered
- Create Linux & Windows VM instances
- SSH via Cloud Shell / Browser SSH
- Install web server (nginx / Apache)
- Create snapshots & custom images
- Resize persistent disks
- Use startup scripts
- Internal vs external IPs and firewall rules
- Service account usage on VM

---

## Files in this folder
- `steps.md` — step-by-step actions I followed
- `commands.md` — exact commands I executed
- `screenshots/` — visual evidence of console, SSH, web page, snapshot

---

## Evidence (screenshots)
- `vm-created.png` — VM list with external IP
- `ssh-connected.png` — browser SSH terminal connected
- `nginx-installed.png` — service status / curl output
- `site-working.png` — nginx default page in browser
- `snapshot-created.png` — snapshot list showing snapshot name

---

## Notes
- I did this using a sandbox account (Pluralsight / GCP free tier).  
- I did NOT store any service account keys or credentials in this repo. (Never commit secrets.)

