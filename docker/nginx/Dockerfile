FROM nginx:1.18-alpine
MAINTAINER CastleDigital

RUN addgroup -g 1000 app \
 && adduser -G app -u 1000 -h /var/www -s /bin/bash -S app
RUN touch /var/run/nginx.pid
RUN mkdir /sock

RUN apk add --no-cache \
  curl \
  nss-tools \
  openssl

COPY ./conf/nginx.conf /etc/nginx/
COPY ./conf/default.conf /etc/nginx/conf.d/

RUN mkdir -p /etc/nginx/html /var/www/html \
  && chown -R app:app /etc/nginx /var/www /var/cache/nginx /var/run/nginx.pid /sock

EXPOSE 8443

USER root

VOLUME /var/www

WORKDIR /var/www/html