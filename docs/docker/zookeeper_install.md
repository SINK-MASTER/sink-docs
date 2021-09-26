## Docker zookeeper安装

- 拉取镜像
```shell script
docker pull zookeeper:3.7.0
```

- 运行
```shell script
docker run --name zookeeper -d -p 2181:2181 -p 2888:2888 -p 3888:3888 -p 8001:8080
```