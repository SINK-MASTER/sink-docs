- 检查是否已安装
```shell script
rpm -qa | grep mysql

rpm -e --nodeps mysql-libs-5.1.73-5.el6_6.x86_64 #卸载

grep mysql #验证是否已删除完毕
whereis mysql
find / -name mysql #删除相关目录

cat /etc/group | grep mysql
cat /etc/passwd | grep mysql
#检查mysql用户组和用户是否存在，如果没有，则创建
groupadd mysql
useradd -r -g mysql mysql
```
- 下载Mysql
```shell script
wget http://repo.mysql.com/mysql57-community-release-el7-8.noarch.rpm
```
- 安装
```shell script
sudo yum install wget

sudo rpm -ivh mysql57-community-release-el7-8.noarch.rpm
sudo yum install mysql-server
```
- 获取初始化密码
```shell script
sudo grep 'temporary password' /var/log/mysqld.log #查看临时密码 如若为空请保证安装前已将mysql相关文件删除干净
systemctl restart mysqld # 重启服务
systemctl status mysqld # 查看服务执行状态
grep 'temporary password' /var/log/mysqld.log #再次查看临时密码
```
- 密码更改
```shell script
sudo mysql_secure_installation #输入刚才的临时密码 All done!表示配置已经完成

mysqladmin -u root password '123456'
vim /etc/my.cnf #根目录的\etc\my.cnf文件中添加一行skip-grant-tables

systemctl restart mysqld.service #重启服务

mysql
update mysql.user set authentication_string=password('123456') where user='root';
flush privileges;
```
- 远程访问
```shell script
#连接数据库报错：1130-Host 'xxx' is not allowed to connect to this MySQL server解决
mysql -u root -p #连接服务器
show databases; #看当前所有数据库
#You must reset your password using ALTER USER statement before executing this statement.
alter user user() identified by '123456';

use mysql; #进入mysql数据库
select 'host' from user where user='root'; #查询下你的用户名为root下host字段的参数
update user set host ='%'where user ='root';
flush privileges; # 一定记得刷新
```
- 开启关闭忽略表名大小写
```shell script
vim /etc/my.cnf
lower_case_table_names=1 # 1、关闭 0开启
service mysqld restart
```