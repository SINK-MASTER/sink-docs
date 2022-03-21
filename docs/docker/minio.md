- 镜像拉取
```shell script
docker pull minio/minio:latest
```

- 启动服务
> 容器内部端口: 9000(API调用) 9001(控制台访问)

```shell script
docker run --name minio -p 8010:9000 -p 8011:9001 \
-d -v /home/docker/minio/data/:/data \
-e "MINIO_ACCESS_KEY=admin" \
-e "MINIO_SECRET_KEY=admin123" \
minio/minio:latest server /data --console-address :9001
```

- 访问
> 访问地址 127.0.0.1:8010
![](../images/minio/minio_01.png)