# NGINX + Elastisearch


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

```ini
log_format catalog '$remote_addr - $remote_user [$time_local] "$request" $status';
```

```ini
awk -F\" '($2 ~ ""){print $1}' elastic_access.log | awk '{print $1}' | sort | uniq -c | sort -nr
```
