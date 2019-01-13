### 安装PHP
```bash
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
yum -y remove php*

yum -y install php72w php72w-cli php72w-fpm php72w-common php72w-devel 
# or
yum -y install php72w php72w-cli php72w-fpm php72w-common php72w-devel php72w-embedded php72w-gd php72w-mbstring php72w-mysqlnd php72w-opcache php72w-pdo php72w-xml

systemctl enable php-fpm.service
systemctl start php-fpm.service
php -r "phpinfo();" | grep php\.ini
php -v
```


### nginx 配置
```nginx
server
    {
        listen 80;
        server_name test.com ;
        index index.html index.htm index.php default.html default.htm default.php;
        root  /home/wwwroot/laravel/public;
        location / {
            try_files $uri $uri/ /index.php?$query_string;
           }

        location ~ \.php$ {
            try_files $uri /index.php =404;
            fastcgi_split_path_info ^(.+\.php)(/.+)$;
            fastcgi_pass 127.0.0.1:9000;
            fastcgi_index index.php;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            include fastcgi_params;
        }
        location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$
        {
            expires      30d;
        }

        location ~ .*\.(js|css)?$
        {
            expires      12h;
        }

        location ~ /.well-known {
            allow all;
        }

        location ~ /\.
        {
            deny all;
        }

        access_log  /home/wwwlogs/laravel.log;
    }
```