# Laverna docker container

[Laverna](http://laverna.cc) is a note taking web application written in JavaScript. It's built to be an open source alternative to Evernote.
This is a [Docker](https://docker.com) compose configuration to setup your own laverna server.

## Setup

This setup includes:

laverna_proxy
* supervisord
* nginx

laverna_web
* supervisord
* nginx
* laverna

## Using the containers

Generate the certificates:

```bash
$ cd proxy/certs/
$ openssl req -x509 -nodes -days 365 -newkey rsa:4096 -keyout cert.key -out cert.crt
```

Customize the Nginx configuration:
```bash
$ vim proxy/sites-enabled/proxy
```

Install docker-compose and start the containers:
```bash
$ docker-compose up
```
