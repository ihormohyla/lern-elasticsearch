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

[Zabbix](https://zabbix-de.ria.com/charts.php?sid=d20160e114b21a88&form_refresh=1&fullscreen=0&groupid=10&hostid=10133&graphid=5258)
