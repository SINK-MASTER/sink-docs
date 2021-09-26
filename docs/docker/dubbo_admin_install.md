### Docker dubbo-admin安装

> 镜像拉取
```shell script
docker pull chenchuxin/dubbo-admin:latest
```

> 启动
```shell script
docker run -d \
-p 8002:8080 \
-e dubbo.registry.address=zookeeper://182.61.20.52:2181 \
-e dubbo.admin.root.password=root \
-e dubbo.admin.guest.password=root \
chenchuxin/dubbo-admin 
```