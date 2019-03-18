# NGINX

## リバプロ設定

/etc/nginx/conf.d に xxxxx.conf を作成
こんなの

```
server {
    listen       80;
    listen       8080;
    server_name  localhost;
    location / {
        proxy_pass http://localhost:9200/;
        auth_basic "Restricted";
        auth_basic_user_file /etc/nginx/.htpasswd;
        proxy_set_header Authorization  "";
    }
}
```
