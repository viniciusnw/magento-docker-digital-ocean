FROM nginx:1.18-alpine
MAINTAINER CastleDigital

RUN touch /var/run/nginx.pid

RUN apk add --no-cache \
  curl \
  nss-tools \
  openssl

COPY ./conf/nginx.conf /etc/nginx/
COPY ./conf/default.conf /etc/nginx/conf.d/

RUN mkdir -p /etc/nginx/html /var/www/html

EXPOSE 8443

WORKDIR /var/www/html