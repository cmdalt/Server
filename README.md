# Debian Server 11

# Update Packages

```
apt update && apt upgrade
```
# Rust
```
sudo apt install build-essential
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
Environment=PATH=var/www/nirde/yeww/dist/
ExecStart=/var/www/nirde/target/release/nirde

[Install]
WantedBy=multi-user.target
```
# Actic
```
use actix_files as fs;
use actix_web::{App, HttpServer,Responder,HttpResponse,get};

use std::env;
use std::path::Path;

#[get("/port")]
async fn hello() -> impl Responder {
    let port = env::var("PORT").unwrap_or_else(|_| "8080".to_string());
    HttpResponse::Ok().body(port)
}

#[actix_web::main]
async fn main() -> std::io::Result<()> {

let port = env::var("PORT").unwrap_or_else(|_| "8080".to_string());

let static_path = env::var("PATH").unwrap_or_else(|_| "static".to_string());

    HttpServer::new(move || {
        App::new()
        .service(hello)
        .service(
            fs::Files::new("/",
                Path::new(&format!("{}",static_path)))
                .index_file("index.html").use_last_modified(true),
        )
    })
    .bind(format!("127.0.0.1:{}", port))?
    .run()
    .await
}
```

```
use actix_files::Files;
use actix_web::{App, HttpServer};

#[actix_web::main]
async fn main() -> std::io::Result<()> {
    HttpServer::new(|| {
        App::new()
        .service(Files::new("/", "/var/www/nirde/dist").index_file("index.html"))
    })
    .bind(("0.0.0.0", 8080))?
    .run()
    .await
}
```

# CertBot Encrypt SSL/TLS

```
apt-get update
sudo apt-get install certbot
apt-get install python3-certbot-nginx
nginx -t && nginx -s reload
sudo certbot --nginx -d example.com -d www.example.com
```
