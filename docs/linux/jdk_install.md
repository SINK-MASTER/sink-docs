- 检查是否安装
```shell script
java -version
```
- 拷贝到指定安装目录
```shell script
cp -r /home/download/jdk-8u221-linux-x64.tar.gz /usr/local/java/
```
- 解压操作
```shell script
cd /usr/local/java/ #切换到指定目录
tar -zxvf jdk-8u221-linux-x64.tar.gz #解压文件
```
- 配置环境变量
```shell script
export JAVA_HOME=/usr/local/java/jdk1.8.0_221/
export JRE_HOME=/$JAVA_HOME/jre
export CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin

source /etc/profile #更新配置生效
```
- 验证是否成功
```shell script
java -version

#java version "1.8.0_221"
#Java(TM) SE Runtime Environment (build 1.8.0_221-b11)
#Java HotSpot(TM) 64-Bit Server VM (build 25.221-b11, mixed mode)
```
> 出现问题：/lib/ld-linux.so.2: bad ELF interpreter: No such file or director
```shell script
sudo yum install glibc.i686
```