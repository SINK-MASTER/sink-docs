## zookeeper安装

- 拉取镜像
```shell script
docker pull zookeeper:3.4.14
```

- 运行
```shell script
docker run --name zookeeper -d -p 2181:2181 zookeeper:3.4.14
```

- 问题
> `EndOfStreamException: Unable to read additional data from client, it probably closed the socket: address = /127.0.0.1:64203, session = 0x0`  
> 尝试更新本地项目pom依赖版本与镜像版本一致