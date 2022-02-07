### SSL

Generete SSL
```bash
docker-compose -f docker-compose.certbot.yml run --rm certbot && docker rm -vf $(docker ps -aq)
openssl dhparam -dsaparam -out ./docker/certbot/conf/live/dhparam.pem 4096
```

Renew
```bash
docker-compose -f docker-compose.certbot-renew.yml run --rm certbot
```

### Setup
bin/setup url

### Start
bin/start

### Recover DB
```sql
UPDATE `core_config_data` SET `value` = 'https://url/' WHERE `core_config_data`.`config_id` = 381;
UPDATE `core_config_data` SET `value` = 'https://url/' WHERE `core_config_data`.`config_id` = 4;
UPDATE `core_config_data` SET `value` = 'elasticsearch' WHERE `core_config_data`.`config_id` = 1;
UPDATE `core_config_data` SET `value` = '9200' WHERE `core_config_data`.`config_id` = 2;
```