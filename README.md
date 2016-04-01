# Laverna docker container

[Laverna](http://laverna.cc) is a note taking web application written in JavaScript. It's built to be an open source alternative to Evernote.
This is a [Docker](https://docker.com) compose configuration to setup your own laverna server.

## Setup

This setup includes:

laverna_proxy
* supervisord
* nginx (reverse proxy)

laverna_web
* supervisord
* nginx (web server)
* laverna

## Generate the certificates with letsencrypt

* Install dependencies
```bash
# apt-get install nginx git bc
# git clone https://github.com/letsencrypt/letsencrypt /opt/letsencrypt
```

* add the following lines to **/etc/nginx/sites-available/default**
```bash
location ~ /.well-known {
        allow all;
}
```

* restart nginx
```bash
# systemctl restart nginx
```

* request the certificate
```bash
# cd /opt/letsencrypt
# ./letsencrypt-auto certonly -a webroot --webroot-path=/usr/share/nginx/html -d notes.example.com
```

* copy the generated certificates under laverna/proxy/certs
```bash
# cd /etc/letsencrypt/live/notes.example.com
# cp fullchain.pem /path/to/laverna/proxy/certs
# cp privkey.pem /path/to/laverna/proxy/certs
```

* generate strong DH group
```bash
# openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
# cp /etc/ssl/certs/dhparam.pem /path/to/laverna/proxy/certs
```

## Use the containers

Customize the nginx configuration:
```bash
$ cd laverna
$ vim proxy/sites-enabled/proxy
```

Install docker-compose and start the containers:
```bash
$ docker-compose up -d
```
