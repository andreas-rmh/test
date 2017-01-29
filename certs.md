# Setup Let's encrypt

## Install certbot-auto
```bash
 $ cd /usr/local/sbin
 $ sudo wget https://dl.eff.org/certbot-auto
 $ chmod a+x /usr/local/sbin/certbot-auto
```

## Nginx config
```
server {
        . . .
        location ~ /.well-known {
                allow all;
        }
        . . .
}
```

## Require cert
```bash
 $ certbot-auto certonly -a webroot --webroot-path=/usr/share/nginx/html -d example.com -d www.example.com
```

## Generate Diffie-Hellman group
```bash
 $ sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
```

## Nginx config
```
server {
    listen 80;
    server_name example.com www.example.com;
    return 301 https://$host$request_uri;
}

server {
  listen 443 ssl;

  server_name example.com www.example.com;

  ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
  ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;

   ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
          ssl_prefer_server_ciphers on;
          ssl_dhparam /etc/ssl/certs/dhparam.pem;
          ssl_ciphers 'ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA';
  ssl_session_timeout 1d;
  ssl_session_cache shared:SSL:50m;
  ssl_stapling on;
  ssl_stapling_verify on;
  add_header Strict-Transport-Security max-age=15768000;
}
```
## Analyze
Use Qualys SSL Labs Report: https://www.ssllabs.com/ssltest/analyze.html?d=example.com

## Renewal
```bash
 $ certbot-auto renew
```

## Add to cron
```bash
 $ sudo crontab -e
```
# Add the following lines:
```
 crontab entry
 30 2 * * 1 /usr/local/sbin/certbot-auto renew >> /var/log/le-renew.log
 35 2 * * 1 /etc/init.d/nginx reload
```


[Source](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-14-04)
