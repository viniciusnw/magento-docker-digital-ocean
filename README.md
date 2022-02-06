### SSL
docker-compose -f docker-compose.certbot.yml run --rm certbot && docker rm -vf $(docker ps -aq)
docker-compose -f docker-compose.certbot-renew.yml run --rm certbot

### Setup
bin/setup url

### Start
bin/start