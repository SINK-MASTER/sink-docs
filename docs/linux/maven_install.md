> 设置配置maven配置 修改/maven/conf/setting.xml 文件配置信息 指向nexus

- 下载
```shell script
wget http://mirrors.cnnic.cn/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz
cp -r /home/download/apache-maven-3.3.9-bin.tar.gz /use/local/
tar -zxvf apache-maven-3.3.9-bin.tar.gz 
mv apache-maven-3.3.9-bin.tar.gz maven 
```
- 修改配置
```shell script
vim /etc/profile
export MAVEN_HOME=/usr/local/maven
export PATH=$PATH:$MAVEN_HOME/bin
source /etc/profile
```