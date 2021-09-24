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