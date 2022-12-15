# websocket-cell-game
Mini local game => AWS


NGINX reverse proxy:


map $http_upgrade $connection_upgrade {

    default upgrade;

    '' close;
}

upstream websocket {

    server 127.0.0.1:7676;

}

server {

    listen 8080 ssl;
    
    location / {
    
    proxy_pass https://websocket;
    
    proxy_http_version 1.1;
    
    proxy_set_header Upgrade $http_upgrade;
    
    proxy_set_header Connection $connection_upgrade;
    
}

    add_header Strict-Transport-Security "max-age=31536000";
    
    ssl on;
    
    ssl_certificate /home/ubuntu/ssl/cert.crt;
    
    ssl_certificate_key /home/ubuntu/ssl_cert.key;
    
    ssl_prefer_server_ciphers on;
    
    
}
