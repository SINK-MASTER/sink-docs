- 拉取镜像
```shell script
docker pull sonatype/nexus
```

- 启动
```shell script
docker run -d --name nexus -p 8008:8081 sonatype/nexus:latest
```