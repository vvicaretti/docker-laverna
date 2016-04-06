# Laverna docker container

[Laverna](http://laverna.cc) is a note taking web application written in JavaScript. It's built to be an open source alternative to Evernote.
This is a [Docker](https://docker.com) compose configuration to setup your own laverna server.

## Setup

This setup includes:

laverna:proxy
* supervisord
* nginx (reverse proxy)

laverna:web
* supervisord
* nginx (web server)
* laverna

## Generate the certificates with letsencrypt

NOTE: these commands needs to be run on the docker host

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

* edit the docker-compose.yml config
```bash
sed -i -e 's/notes.examples.com/your.site.com/' docker-compose.yml
```

* generate strong DH group
```bash
# openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
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
