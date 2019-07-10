## gunicorn
---
.py
http://gunicorn.org/

https://pypi.org/project/gunicorn/


```sh
pip install gunicorn
gunicorn --workers=2 test:app
```

```conf
// nginx.conf
worker_processes 1;

user nobody nogroup;
error_log /var/log/nginx/error.log warn;
pid /var/run/nginx.pid;

events {
  worker_connections 1024;
  accept_mutex off;
}

http {
  include mime.type;
  default_type application/octet-stream;
  access_log /var/log/nginx/access.log combined;
  sendfile on;
  
  upstream app_server {
    server unix:/tmp/gunicorn.sock fail_timeout=0;
    # server 192.168.0.7:8000 fail_timeout=0;
  }
  
  server {
    listen 80 default_server;
    return 444;
  }
  
  server {
    listen 80;
    client_max_body_size 4G;
    
    server_name example.com www.example.com;
    
    root /path/to/app/current/public;
  }
}


```

```
```

