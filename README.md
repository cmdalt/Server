# Debian Server 11

### Update Packages

```
apt update && apt upgrade
```

### Install Nginx
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
                proxy_pass http://0.0.0.0:8080;
                proxy_buffering off; # Single Page App work faster with it
                proxy_set_header X-Real-IP $remote_addr;
        }
}
```

# Systemd 
### /etc/systemd/system/name.service
```
[Unit]
Description=Foo

[Service]
Environment=PORT=8080
Environment=PATH=/var/www/nirde/yeww/dist/
ExecStart=/var/www/nirde/target/release/nirde

[Install]
WantedBy=multi-user.target
```


```

# CertBot Encrypt SSL/TLS

```
apt-get update
sudo apt-get install certbot
apt-get install python3-certbot-nginx
nginx -t && nginx -s reload
sudo certbot --nginx -d example.com -d www.example.com
```
