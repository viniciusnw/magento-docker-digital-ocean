### SSL

Generete SSL
```
docker-compose -f docker-compose.certbot.yml run --rm certbot && docker rm -vf $(docker ps -aq)
openssl dhparam -dsaparam -out ./docker/certbot/conf/live/dhparam.pem 4096
```

Renew
```
docker-compose -f docker-compose.certbot-renew.yml run --rm certbot
```

### Setup
bin/setup url

### Start
bin/start