# Haproxy
```
global
   ssl-default-bind-options no-sslv3 no-tls-tickets force-tlsv12
   ssl-default-bind-ciphers AES128+EECDH:AES128+EDH

frontend http-in
      mode http
      option httplog
      option forwardfor
      option http-server-close
      option httpclose
      bind 192.0.2.10:80
      redirect scheme https code 301 if !{ ssl_fc }

frontend https-in
    option httplog
    option forwardfor
    option http-server-close
    option httpclose
    rspadd Strict-Transport-Security:\ max-age=31536000;\ includeSubDomains;\ preload
    rspadd X-Frame-Options:\ DENY
    bind 192.0.2.10:443 ssl crt /etc/haproxy/haproxy.pem ciphers AES128+EECDH:AES128+EDH force-tlsv12 no-sslv3
```
