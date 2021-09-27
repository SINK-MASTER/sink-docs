### Docker dubbo-admin安装

> 镜像拉取
```shell script
docker pull chenchuxin/dubbo-admin:latest
```

> 启动
```shell script
docker run -d \
--name duubo-admin \
-p 8002:8080 \
-e dubbo.registry.address=zookeeper://127.0.0.1:2181 \
-e dubbo.admin.root.password=root \
-e dubbo.admin.guest.password=root \
chenchuxin/dubbo-admin 
```

### apache-dubbo-admin

> 镜像拉取
```shell script
docker pull apache/dubbo-admin:latest
```

> 启动
> `zookeeper 地址注意替换`
```shell script
docker run -d \
--name dubbo-admin \
-v /home/docker/dubbo-admin/data:/data \
-p 8002:8080 \
-e admin.registry.address=zookeeper://127.0.0.1:2181 \
-e admin.config-center=zookeeper://127.0.0.1:2181 \
-e admin.metadata-report.address=zookeeper://127.0.0.1:2181 \
apache/dubbo-admin
```