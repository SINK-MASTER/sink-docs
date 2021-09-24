> web层
```dockerfile
FROM 60.205.187.16:1180/base/java8:1.1
MAINTAINER sink
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

#设置时区
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN sh -c echo 'Asia/Shanghai' >/etc/timezone

RUN mkdir sink-web

ADD target/sink-web*SNAPSHOT.jar ./sink-web/app.jar
ADD target/lib/* ./sink-web/lib/

ENV CLASSPATH ./sink-web/app.jar;./sink-web/lib/*;
ENTRYPOINT exec java -jar ./sink-web/app.jar ${env_tag}
```

> server层
```dockerfile
FROM 60.205.187.16:1180/base/java8:1.1
MAINTAINER sink
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

#设置时区
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN sh -c echo 'Asia/Shanghai' >/etc/timezone

RUN mkdir sink-query-server

ADD target/query-server*SNAPSHOT.jar ./sink-query-server/app.jar
ADD target/lib/* ./sink-query-server/lib/

ENV DUBBO_IP_TO_REGISTRY $HOSTIP

ENV CLASSPATH ./sink-query-server/app.jar;./sink-query-server/lib/*;
ENTRYPOINT exec java -jar ./sink-query-server/app.jar ${env_tag}
```

> jenkins打包编译脚本
```shell script
DOCKERFILE_PATH=docker
REGISTRY_URL=60.205.187.16:1180
IAMGE_NAME=webapp/sink-web
CONTAINER_NAME=sale-usercenter
LAST_VERSION=$(date +%Y%m%d%H%M%S)
echo '>>> remove old containers'
docker login -u admin -p Sink1234 $REGISTRY_URL

if docker ps -a | grep $IMAGE_NAME; then
    docker rm -f $(docker ps -a | grep $IMAGE_NAME | awk '{print $1}')
fi
echo '>>> remove old image'
#if docker images -a | grep $IAMGE_NAME; then
#    docker rmi -f $(docker images -a | grep $IMAGE_NAME | awk '{print $3}')
#fi
cd /home/jenkins/workspace/sink-web
project_path=$(cd `dirname $0`; pwd)
echo $project_path

cp -rf $DOCKERFILE_PATH/Dockerfile .

echo '>>> build new image'
docker build -t $REGISTRY_URL/$IAMGE_NAME:$LAST_VERSION .
echo '>>> push image to registry'
docker push $REGISTRY_URL/$IAMGE_NAME:$LAST_VERSION
echo '>>> build end'
```