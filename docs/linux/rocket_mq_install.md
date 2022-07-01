# RocketMQ配置

> [官方文档](https://rocketmq-1.gitbook.io/rocketmq-connector/)



## RocketMQ安装

### 下载rocketMQ

> 直接下载官方的编译包

```sh
# Download release from the Apache mirror
$ wget https://archive.apache.org/dist/rocketmq/4.9.3/rocketmq-all-4.9.3-bin-release.zip

# Unpack the release
$ unzip rocketmq-all-4.9.3-bin-release.zip
```

- or

> 下载项目本地编译 clone `https://github.com/apache/rocketmq.git`

```shell
cd rocketmq
# meavn打包
mvn -Prelease-all -DskipTests clean install -U
# 这里的4.9.x是版本号，可能不同，请注意自己的版本
cd distribution/target/rocketmq-4.9.5-SNAPSHOT.zip
```



### 启动服务

> 启动时可以根据实际情况自定义jvm启动参数
>
> `runbroker.sh` `runserver.sh`

```sh
JAVA_OPT="${JAVA_OPT} -server -Xms256m -Xmx256m -Xmn128m"
```



#### 启动NameServer

> 默认端口`9876`

```shell
### start Name Server
nohup sh mqnamesrv & tail -f nohup.out
The Name Server boot success. serializeType=JSON
```



### 停止NameServer

```
sh bin/mqshutdown namesrv
```



### 启动Broker

> 追加`broker.conf`配置

```
namesrvAddr = 本机外网IP:9876
brokerIP1=本机外网IP
waitTimeMillsInSendQueue=400
```

> 启动

```shell
### start Broker
nohup sh mqbroker -n "本机外网IP:9876" autoCreateTopicEnable=true -c ../conf/broker.conf &tail -f nohup.out
The broker[broker-a, 本机外网IP:10911] boot success. serializeType=JSON and name server is 本机外网IP:9876
```



### 停止Broker

```
sh mqshutdown broker
```



---

## RocketMQ Console安装



### 下载RockerMQ Consoel

> clone `https://github.com/apache/rocketmq-dashboard.git`



### 修改配置

```yaml
rocketmq:
  config:
    namesrvAddrs:
      - 本机外网IP:9876
```



### 编译

> 获取docker镜像

```shell
docker pull apacherocketmq/rocketmq-dashboard:latest
```

> 运行

```shell
docker run -d --name rocketmq-dashboard -e "JAVA_OPTS=-Drocketmq.namesrv.addr=127.0.0.1:9876" -p 8080:8080 -t apacherocketmq/rocketmq-dashboard:latest
```

---

> 编译jar

```shell
mvn clean package -Dmaven.test.skip=true
```

> 运行

```shell
java -jar target/rocketmq-dashboard-1.0.1-SNAPSHOT.jar
```