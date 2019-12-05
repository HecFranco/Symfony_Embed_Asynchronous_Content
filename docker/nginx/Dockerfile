FROM nginx:1.13

MAINTAINER Héctor Franco Aceituno <hector.franco.aceituno@mail.com>

ARG nginx_host
ARG password_ssl

RUN apt-get update && apt-get install --no-install-recommends --no-install-suggests -y \
        openssl \
    && rm -rf /var/lib/apt/lists/*

COPY openssl.cnf /etc/ssl/openssl.cnf
RUN sed -i -e "s/NGINX_HOST/$nginx_host/g" /etc/ssl/openssl.cnf

RUN openssl genrsa -des3 -passout pass:$$password_ssl -out /etc/ssl/server.pass.key 2048
RUN openssl rsa -passin pass:$$password_ssl -in /etc/ssl/server.pass.key -out /etc/ssl/server.key
RUN rm /etc/ssl/server.pass.key
RUN openssl req -new -passout pass:$$password_ssl -key /etc/ssl/server.key -out /etc/ssl/server.csr \
    -subj "/C=SP/ST=Spain/L=Spain/O=Symfony/CN=$nginx_host" -config /etc/ssl/openssl.cnf
RUN openssl x509 -req -sha256 -days 365 -in /etc/ssl/server.csr -signkey /etc/ssl/server.key \
    -out /etc/ssl/server.crt -extensions v3_req -extfile /etc/ssl/openssl.cnf

ADD nginx.conf /etc/nginx/

RUN rm /var/log/nginx/access.log /var/log/nginx/error.log