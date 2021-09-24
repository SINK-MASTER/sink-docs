- 安装
```shell script
wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
yum -y install apache-maven
```
- 安装路径查看
```shell script
rpm -ql apache-maven
```
- 修改配置
```shell script
vim /etc/maven/setting.xml
```