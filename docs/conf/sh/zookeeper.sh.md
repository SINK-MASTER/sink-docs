```shell script
#!/bin/bash
#chkconfig:2345 20 90
#description:zookeeper
#processname:zookeeper
export JAVA_HOME=/usr/local/java/jdk1.8.0_221
export ZOO_LOG_DIR=/usr/local/zookeeper/logs
case $1 in
    start) su root /usr/local/zookeeper/bin/zkServer.sh start;;
    stop) su root /usr/local/zookeeper/bin/zkServer.sh stop;;
    status) su root /usr/local/zookeeper/bin/zkServer.sh status;;
    restart) su root /usr/local/zookeeper/bin/zkServer.sh restart;;
    *) echo "require start|stop|status|restart" ;;
esac

```