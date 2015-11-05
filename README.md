# NGINX + Elasticsearch

## Конфиг Nginx
```ini
server {
    listen       9200;
    server_name _;

    error_log  /var/log/nginx/elastic_error.log;
    access_log /var/log/nginx/elastic_access.log catalog;

    location / {
        proxy_pass http://10.1.18.241:9199;
    }
}
```
## Формат лога
```ini
log_format catalog '$remote_addr - $remote_user [$time_local] "$request" $status';
```
## Получение популярных IP
```ini
awk -F\" '($2 ~ ""){print $1}' elastic_access.log | awk '{print $1}' | sort | uniq -c | sort -nr
```

[Zabbix](https://zabbix-de.ria.com/)

## Получение Took Time для экспорта в Zabbix
```ini
curl --silent  -X GET http://localhost:9200/search_index/_search | python -c 'import json,sys;obj=json.load(sys.stdin);print obj["took"]'
```

[Bigdesk](http://couchdb.dom.ria.com:9400/_plugin/bigdesk/#nodes/2L2_4MI9QZCYh5EVPYzVTA)
