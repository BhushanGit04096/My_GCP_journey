# Compute Engine — Commands Reference

This file contains all commands used across all Compute Engine hands-on labs.

---

## 🟩 1. Basic VM + nginx Setup

### Update packages
```bash
sudo apt update -y
```

### Install nginx
```bash
sudo apt install nginx -y
```

### Start & enable nginx
```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

### Check status
```bash
sudo systemctl status nginx --no-pager
```

### Local tests
```bash
curl http://localhost
curl -I http://localhost
```

### Optional: Replace default page
```bash
echo "Hello from lab-vm-nginx" | sudo tee /var/www/html/index.html
curl http://localhost
```

---

## 🟩 2. Internal vs External IP Testing

### Ping internal IP
```bash
ping <VM2_INTERNAL_IP>
```

### Curl internal IP
```bash
curl http://<VM2_INTERNAL_IP>
```

### Curl external IP
```bash
curl http://<VM2_EXTERNAL_IP>
```

---

## 🟩 3. Resize Boot Disk

### Check current disk size
```bash
df -h
```

### Grow disk partition
```bash
sudo growpart /dev/sda 1
```

### Resize filesystem
```bash
sudo resize2fs /dev/sda1
```

### Verify
```bash
df -h
```

---

## 🟩 4. Additional Disk Attachment

### List disks
```bash
lsblk
```

### Format additional disk
```bash
sudo mkfs.ext4 /dev/sdb
```

### Create mount directory
```bash
sudo mkdir /data
```

### Mount disk
```bash
sudo mount /dev/sdb /data
```

### Verify
```bash
df -h
```

### Permanent mount entry (add to /etc/fstab)
```
/dev/sdb   /data   ext4   defaults   0  2
```

---

## 🟩 5. Startup Script Testing

### Manually test script output
```bash
cat /var/www/html/index.html
sudo systemctl status nginx --no-pager
```

---

## 🟩 6. Static IP Verification

### Show instance details
```bash
curl http://metadata.google.internal/computeMetadata/v1/instance/network-interfaces/0/access-configs/0/external-ip \
  -H "Metadata-Flavor: Google"
```

---

## 🟩 7. Custom Firewall Rule (Port 8080)

### Run simple netcat server
```bash
echo "Hello from port 8080" | sudo nc -l -p 8080
```

---

## 🟩 8 Service Accounts + IAM Testing

### Test Storage access (expected fail / pass)
```bash
gsutil ls
```

---

## 🟩 9. Metadata Server

### Access metadata root
```bash
curl -H "Metadata-Flavor: Google" \
"http://metadata.google.internal/computeMetadata/v1/"
```

### Access instance hostname
```bash
curl -H "Metadata-Flavor: Google" \
"http://metadata.google.internal/computeMetadata/v1/instance/hostname"
```

### Access instance ID
```bash
curl -H "Metadata-Flavor: Google" \
"http://metadata.google.internal/computeMetadata/v1/instance/id"
```

---

## 🟩 10. Create VM From Custom Image (Console)

(No terminal commands — done through console.)

---

# ✔ End of Commands File

This covers all Compute Engine topics required for interviews & production readiness.
