### 准备 Nginx + PHP 环境

-   安装 Nginx
    
    使用  `yum`  安装 Nginx：
    
    yum install nginx
    
    修改  /etc/nginx/nginx.conf  文件为如下内容：
    
    user nginx;
    worker_processes auto;
    error_log /var/log/nginx/error.log;
    pid /run/nginx.pid;
    
    include /usr/share/nginx/modules/*.conf;
    
    events {
        worker_connections 1024;
    }
    
    http {
        log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                          '$status $body_bytes_sent "$http_referer" '
                          '"$http_user_agent" "$http_x_forwarded_for"';
    
        access_log  /var/log/nginx/access.log  main;
    
        sendfile            on;
        tcp_nopush          on;
        tcp_nodelay         on;
        keepalive_timeout   65;
        types_hash_max_size 2048;
    
        include             /etc/nginx/mime.types;
        default_type        application/octet-stream;
        include /etc/nginx/conf.d/*.conf;
    
        server {
            listen       80;
            server_name  127.0.0.1;
            root         /var/www/html;
            index index.php index.html
            error_page  404              /404.html;
            location = /40x.html {
            }
            error_page   500 502 503 504  /50x.html;
            location = /50x.html {
            }
            location ~ .php$ {
                root           /var/www/html;
                fastcgi_pass   127.0.0.1:9000;
                fastcgi_index  index.php;
                fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
                include        fastcgi_params;
            }
            location ~ /.ht {
                deny  all;
            }
        }
    }
    
    启动 Nginx 并设置为开机启动：
    
    service nginx start
    chkconfig nginx on
-   安装 PHP
    
    使用  `yum`  安装 php-fpm：
    
    yum install php php-gd php-fpm php-mcrypt php-mbstring php-mysql php-pdo
    
    启动 php-fpm 并设置为开机启动：
    
    service php-fpm start
    chkconfig php-fpm on
    

### 创建项目

-   下载安装 Composer
    
    Composer 是 PHP 的一个依赖管理工具，推荐使用 Composer 创建 ShowDoc 项目。
    
    执行如下命令
    
    安装 Composer
    
    ：
    
    curl -sS https://getcomposer.org/installer | php
    mv composer.phar /usr/local/bin/composer

设置 Composer 使用国内镜像

执行命令

设置 Composer 使用国内镜像

为了避免访问国外网络导致的延迟，推荐使用国内镜像源

：

composer config -g repo.packagist composer https://packagist.phpcomposer.com

已完成，下一步

使用 Composer 创建项目

执行命令创建项目：

cd /var/www/html/ && composer create-project  showdoc/showdoc

下一步

设置 showdoc 目录写权限

执行命令赋予 showdoc 下部分目录的写权限

chmod a+w showdoc/install
chmod a+w showdoc/Sqlite
chmod a+w showdoc/Sqlite/showdoc.db.php
chmod a+w showdoc/Public/Uploads/
chmod a+w showdoc/Application/Runtime
chmod a+w showdoc/server/Application/Runtime
chmod a+w showdoc/Application/Common/Conf/config.php
chmod a+w showdoc/Application/Home/Conf/config.php

创建完毕，您现在可以通过浏览器访问  [http://203.195.219.61/showdoc/install/](http://203.195.219.61/showdoc/install/ "null")  ，进行语言的选择以后即可通过  [http://203.195.219.61/showdoc](http://203.195.219.61/showdoc "null")  查看站点效果。
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk2ODM3NTE3Nl19
-->