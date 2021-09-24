```shell script
#!/bin/sh
ulimit -s 256
APP_HOME=${PWD} # 获取当前文件路径
programdir="."

num=$#
temp=$CLASSPATH:$APP_HOME/lib:./
#setting libs path
libs=lib/*  # 指定lib文件
append(){
                temp=$temp":"$1
}

basepath=${PWD}/*
for file in $basepath; do
	echo ${file##*.}
	if [ "${file##*.}" = "jar" ];then
       append $file
    fi
done

for file in $libs;    do
                append $file
done
export CLASSPATH=$temp
# 指定环境 切换配置文件
export activeTag=dev
#export LC_ALL="en_US.UTF-8"
#export CLASSPATH=$CLASSPATH:$APP_HOME/lib
echo $CLASSPATH
JAVA_OPTS="-Xms1024m -Xmx1024m -Xss256K -XX:PermSize=256m -XX:MaxPermSize=512m"
# Spring Mvc 指定启动main方法
nohup java -classpath $CLASSPATH com.sink.query.SinkQueryServerStart > query.out 2>&1 &
# Spring Boot 指定启动Jar文件
nohup java -classpath $CLASSPATH com.sink.query.SinkQueryApplication > query.out 2>&1 &
#tail -f query.out

```