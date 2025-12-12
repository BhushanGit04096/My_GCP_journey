# Commands used — Compute Engine nginx lab

# Update packages
sudo apt update -y

# Install nginx
sudo apt install nginx -y

# Start & enable (usually auto-start)
sudo systemctl start nginx
sudo systemctl enable nginx

# Check nginx status
sudo systemctl status nginx --no-pager

# Quick check from VM
curl -I http://localhost

# (Optional) create a file to show web content
echo "Hello from lab-vm-nginx" | sudo tee /var/www/html/index.html
curl http://localhost

