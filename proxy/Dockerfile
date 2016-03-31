FROM debian:latest

MAINTAINER vincent@autistici.org

RUN apt-get update

RUN apt-get install -y nginx supervisor

RUN rm /etc/nginx/sites-enabled/default

RUN rm -rf /var/lib/apt/lists/* 

ADD laverna.conf /etc/supervisor/conf.d/laverna.conf

CMD ["/usr/bin/supervisord"]

EXPOSE 80 443
