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
3. create conf.d directory 
`sudo mkdir conf.d`
3.1 create configuration file for each domain or subdomain
`sudo vi dashboard.conf`
4. create directory for each website
`sudo mkdir /var/www/dashboard`
4.1 change own of directory 
`sudo chown -R /var/www/dashboard`
4.2 change directory mode for everyone can be read
`sudo chmod -R 755 /var/www/dashboard`

## Regular Maintenance
### update server
`sudo apt update`
`sudo apt upgrade`
### automatic update security update
`sudo apt install unattended-upgrades apt-listchanges`
### update unattended 
`sudo dpkg-reconfigure -plow unattended-upgrades`
