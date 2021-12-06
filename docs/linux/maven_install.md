> 设置配置maven配置 修改/maven/conf/setting.xml 文件配置信息 指向nexus

- 下载
```shell script
wget http://mirrors.cnnic.cn/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz
cp -r /home/download/apache-maven-3.3.9-bin.tar.gz /var/local/
tar -zxvf apache-maven-3.3.9-bin.tar.gz 
mv apache-maven-3.3.9-bin.tar.gz maven 
```
- 添加环境变量
```shell script
export MAVEN_HOME=/var/local/maven
export PATH=$PATH:$MAVEN_HOME/bin
source /etc/profile
```

- 修改配置
> [参考文件](/conf/maven/setting.xml.md)
```shell script
vim  /var/local/maven/conf/setting.xml
```