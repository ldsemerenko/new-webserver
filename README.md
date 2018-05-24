# New webserver

Scripts and config files to quickly start a new webserver that has:

- ufw
- letsenscrypt ssl cert
- Diffie-Hellman parameters
- nginx with ssl properly configured

Assumes you are logged in as root.

# UFW

    ufw default deny incoming
    ufw default allow outgoing
    ufw allow 22  # ssh
    ufw allow 443 # https
    ufw allow 80  # http
    ufw enable

# Letsencrypt

    mkdir /lego
    cd /lego
    wget https://github.com/xenolf/lego/releases/download/v0.4.1/lego_linux_amd64.tar.xz
    tar -xf lego_linux_amd64.tar.xz
    mv lego_linux_amd64 lego
    ./lego --email="EMAIL" --domains="DOMAIN" -a run

# Nginx

    apt-get install nginx # todo: nginx official repo
    openssl dhparam -out /etc/nginx/dhparam.pem 2048 # Diffie-Hellman parameters
    cd /etc/nginx/conf.d
    wget https://raw.githubusercontent.com/askmike/new-webserver/master/site.conf
    # edit nginx conf with your site and api
    service nginx configtest
    service nginx restart
    

# nodejs

    curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
    # follow instructions in terminal
    nvm install 10
