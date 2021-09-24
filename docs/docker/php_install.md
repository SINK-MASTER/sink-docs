- 下载镜像
> 下载nginx镜像
```shell script
docker pull nginx
```
> 下载PHP镜像
```shell script
docker pull php:7.1.0-fpm
```

- 建立本地目录
```shell script
mkdir -p /docker/www
mkdir -p /docker/nginx/conf.d
```

- 编辑default.conf
```shell script
vim /docker/nginx/conf.d/default.conf
```
> 添加配置
```based
server {
  listen  80 default_server;
  server_name _;
  root   /usr/share/nginx/html;
 
  location / {
   index index.html index.htm index.php;
   autoindex off;
  }
  location ~ \.php(.*)$ {
   root   /var/www/html/;
   fastcgi_pass 172.18.0.2:9000;
   fastcgi_index index.php;
   fastcgi_split_path_info ^((?U).+\.php)(/?.+)$;
   fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
   fastcgi_param PATH_INFO $fastcgi_path_info;
   fastcgi_param PATH_TRANSLATED $document_root$fastcgi_path_info;
   include  fastcgi_params;
  }
}
```

- 启动php镜像
```shell script
docker run -p 9000:9000 --name php \
-v /docker/www/:/var/www/html/ \
--privileged=true \
-d php:7.1.0-fpm
```

- 查看php镜像地址IP
> 修改default.conf配置文件，使fastcgi_pass的值为 172.18.0.2:9000
```shell script
docker inspect --format='{{.NetworkSettings.IPAddress}}' myphp
```

- 启动nginx镜像
```shell script
docker run -p 80:80 --name mynginx \
-v /docker/www:/usr/share/nginx/html \
-v /docker/nginx/conf.d:/etc/nginx/conf.d \
--privileged=true \
-d nginx
```

- 生成php测试文件info.php
> 浏览器访问 http://101.132.153.197/info.php
```based
echo "<?php phpinfo();" > /docker/www/info.php
```

- Docker容器中安装GD库 
```shell script
apt-get update
```
```shell script
apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libpng12-dev
```
```shell script
docker-php-ext-install -j$(nproc) iconv mcrypt
```
```shell script
docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
```
```shell script
docker-php-ext-install -j$(nproc) gd
```

- Docker容器中安装pdo、pdo_mysql扩展
- pdo
```shell script
docker-php-ext-install pdo
```
- pdo_mysql
```shell script
docker-php-ext-install pdo_mysql
```

- 出现问题
> `[2020-09-03T13:56:05+08:00][error] [0]Call to undefined function app\install\controller\mysqli_connect()`
```shell script
docker-php-ext-install pdo_mysql
```
```shell script
docker-php-ext-install mysqli
```
> 重启容器
>
>出现 mkdir() Permission denied 问题
```shell script
chmod  -R 777 runtime
```