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
UPDATE `core_config_data` SET `value` = 'https://url/' WHERE `core_config_data`.`path` = 'web/secure/base_url';
UPDATE `core_config_data` SET `value` = 'https://url/' WHERE `core_config_data`.`path` = 'web/unsecure/base_url';
UPDATE `core_config_data` SET `value` = 'elasticsearch' WHERE `core_config_data`.`path` = 'catalog/search/elasticsearch7_server_hostname';
UPDATE `core_config_data` SET `value` = '9200' WHERE `core_config_data`.`path` = 'catalog/search/elasticsearch7_server_port';
```

```bash
bin/magento se:up ; bin/magento se:di:co
bin/magento indexer:reset ; bin/magento indexer:reindex
```

### Cron Install
```bash
docker-compose run -d cron
docker exec -it magento-docker-digitalocean_cron_1 bash
bin/magento cron:install --force
service cron start
```