```dockerfile
FROM 127.0.0.1:1180/base/java8:1.1
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