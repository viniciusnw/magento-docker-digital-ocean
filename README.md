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

### Turn off Apache
```bash
sudo /etc/init.d/apache2 stop
```
### Setup
```bash
bin/setup url
```
### Start
```bash
bin/start
```
### After recover DB
```sql
UPDATE `core_config_data` SET `value` = 'https://url/' WHERE `core_config_data`.`config_id` = 381;
UPDATE `core_config_data` SET `value` = 'https://url/' WHERE `core_config_data`.`config_id` = 4;
UPDATE `core_config_data` SET `value` = 'elasticsearch' WHERE `core_config_data`.`config_id` = 1;
UPDATE `core_config_data` SET `value` = '9200' WHERE `core_config_data`.`config_id` = 2;
```

```bash
bin/magento se:up ; bin/magento se:di:co
```