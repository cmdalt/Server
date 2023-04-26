# Debian Server 11

### sudo apt update
### sudo apt upgrade
### sudo apt install nginx
### sudo apt install ufw - sudo ufw allow 'Nginx HTTP' - sudo ufw allow 'OpenSSH'
sudo nano /etc/nginx/sites-available/your_domain

server {
    listen 80;
    listen [::]:80;

    server_name your_domain www.your_domain;
        
    location / {
        proxy_pass app_server_address;
        include proxy_params;
    }
}

sudo ln -s /etc/nginx/sites-available/your_domain /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx


