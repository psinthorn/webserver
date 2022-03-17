# webserver
Deploy web server with docker

## How to deploy caddy web server
1. install or run caddy 
2. configurations
2.1 backup Caddyfile to Caddyfile.dist
`cd /etc/caddy`
`sudo mv Caddyfile Caddyfile.dist`
2.2 create new Caddyfile and configuration 
`sudo vi Caddyfile`
>{
    email   psinthorn@gmail.com
}

(static) {
        @static {
                file
                path *.ico *.css *.js *.gif *.jpg *.jpeg *.png *.svg *.woff *.json
        }
        header @static Cache-Control max-age=5184000
}

(security) {
        header {
                # enable HSTS
                Strict-Transport-Security max-age=31536000;
                # disable clients from sniffing the media type
                X-Content-Type-Options nosniff
                # keep referrer data off of HTTP connections
                Referrer-Policy no-referrer-when-downgrade
        }
}

>import conf.d/*.conf`