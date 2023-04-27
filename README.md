# Debian Server 11

# Update Packages

```
apt update && apt upgrade
```

# Install Nginx
```
sudo apt install nginx
```
### /etc/nginx/sites-available
### /etc/nginx/sites-enabled
### sudo ln -s /etc/nginx/sites-available/yourdomain.com.conf /etc/nginx/sites-enabled/

```
server {
        listen 80;
        listen [::]:80;

        server_name nirde.com www.nirde.com;

        location / {
                proxy_pass http://127.0.0.1:8000;
                include proxy_params;
        }
}
```

# Install UFW

```
sudo apt install ufw
```
```
sudo ufw allow ssh
```
```
sudo ufw allow 'Nginx Full'
```

# Systemd 
### /etc/systemd/system/name.service
```
[Unit]
Description=Foo

[Service]
Environment=PORT=8080
Environment=PATH=var/www/nirde/yeww/dist/
ExecStart=/var/www/ozgur/ozgur

[Install]
WantedBy=multi-user.target
```

# Hosts Domain 
### /etc/hosts
```
82.165.71.65    0zgur.com www.0zgur.com
127.0.0.1       localhost.localdomain localhost
127.0.1.1       localhost
```
# Rust
```
sudo apt install build-essential
```

