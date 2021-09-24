-Linux下启动Jar文件
> 编写脚本文件参考[start.sh](/conf/sh/start.sh.md)
>
- Spring Mvc 指定启动main方法
> 参考文件[SinkQueryServerStart](/conf/java/SinkQueryServerStart.java.md)
```base
nohup java -classpath $CLASSPATH com.sink.query.SinkQueryServerStart > query.out 2>&1 &
```
- Spring Boot 指定启动Jar文件
```base
nohup java -classpath $CLASSPATH com.sink.query.SinkQueryApplication > query.out 2>&1 &
```