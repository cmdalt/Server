# Server Settings

### Update Packages

```
apt update && apt upgrade
```

### Install Nginx
```
sudo apt install nginx
```
```
nano /etc/nginx/sites-available/domain.conf
```

```
server {
        listen 80;
        listen [::]:80;

        server_name domain.com www.domain.com;

        location / {
                proxy_pass http://0.0.0.0:8080;
                proxy_buffering off; # Single Page App work faster with it
                proxy_set_header X-Real-IP $remote_addr;
        }
}
```


```
sudo ln -s /etc/nginx/sites-available/domain.conf /etc/nginx/sites-enabled/
```



### Systemd 

```
nano /etc/systemd/system/domain.service
```




```
[Unit]
Description=domain

[Service]
Environment=PORT=8000
Environment=PATH=/var/www/domain/public/
ExecStart=/var/www/domain/server

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
