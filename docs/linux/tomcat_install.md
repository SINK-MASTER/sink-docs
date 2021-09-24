- 复制安装文件到指定目录
```shell script
cp -r /home/download/apache-tomcat-8.5.53.tar.gz /usr/local/tomcat/
```
- 进入目录
```shell script
cd /usr/local/tomcat/
```
- 解压安装包
```shell script
tar -zxvf apache-tomcat-8.5.53.tar.gz cd /usr/local/tomcat/
```
- 配置环境变量
```shell script
export CATALINA_HOME=/usr/local/tomcat/apache-tomcat-8.5.53
export CLASSPATH=.:$JAVA_HOME/lib:$CATALINA_HOME/lib
export PATH=$PATH:$CATALINA_HOME/bin

#更新环境变量
source /etc/profile
```
- 启动Tomcat测试
```shell script
./catalina.sh start
http://${IP}:8080
```
- tomcat启动缓慢
```shell script
vim /usr/local/java/jdk1.8.0_221/jre/lib/security/java.security

securerandom.source=file:/dev/./urandom #修改地址
```
- 配置多个tomcat
```shell script
vim /etc/profile
export TOMCAT_HOME=/home/server/vanessa/
export CATALINA_BASE=/home/server/vanessa/
export CATALINA_HOME=/home/server/vanessa/
source /etc/profile

vim /home/server/vanessa/bin/catalina.sh

#开头处添加
export CATALINA_BASE=$CATALINA_BASE
export CATALINA_HOME=$CATALINA_HOME

./startup.sh start
#访问：http://ip:port
```