- jdk版本选择
```shell script
yum list java*
```
- 安装jdk
```shell script
yum -y install java-1.8.0-openjdk.x86_64
```
- 修改环境变量
```shell script
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.262.b10-0.el7_8.x86_64
export JRE_HOME=/$JAVA_HOME/jre
export CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
```
- 验证
```shell script
java-version
java
```