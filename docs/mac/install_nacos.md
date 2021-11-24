- 下载镜像
```shell script
docker pull nacos/nacos-server:1.4.1
```

- 启动
> `MYSQL_SERVICE_HOST`: 数据库主机地址  
> `MYSQL_SERVICE_DB_NAME`: 数据库名称  
> `MYSQL_SERVICE_USER`: 数据库用户名  
> `MYSQL_SERVICE_PASSWORD`：数据库密码  
> `SPRING_DATASOURCE_PLATFORM`：数据库类型  
> `MYSQL_DATABASE_NUM`: 数据源数量  
> `NACOS_USER`: 登陆账号名称  
> `NACOS_PASSWORD`: 登陆账号密码

- 数据库账号密码在配置文件中添加 如有需要请自行追加启动配置

```shell script
-e MYSQL_SERVICE_USER=root
-e MYSQL_SERVICE_PASSWORD=root
```

- 想要在docker容器内访问到mac上安装到mysql
- 将MYSQL_SERVICE_HOST设置成`host.docker.internal`
- 解析为主机使用的内部 IP 地址的特殊 DNS 名称
 
> 参考文档`https://docs.docker.com/desktop/mac/networking/`
```
docker run \
-d \
--name nacos \
-e MYSQL_SERVICE_HOST=host.docker.internal \
-e MYSQL_SERVICE_DB_NAME=nacos \
-e SPRING_DATASOURCE_PLATFORM=mysql \
-e MYSQL_DATABASE_NUM=1 \
-e NACOS_USER=nacos \
-e NACOS_PASSWORD=nacos \
-p 8848:8848 \
-v /home/docker/nacos/conf:/home/nacos/conf \
-v /home/docker/nacos/logs:/home/nacos/logs \
nacos/nacos-server:1.4.1
```
