- 下载
```shell script
yum -y install memcached.x86_64 
```
- 启动
```shell script
/usr/bin/memcached -m 256 -u root -p 12000 -d
/usr/bin/memcached -m 256 -u root -p 11211 -d
```
- 脚本方式启动
> 创建脚本文件
```shell script
cd /home
touch memcached.sh
chmod a+x memcached.sh
vim memcached.sh
```
> 添加内容
```shell script
/usr/bin/memcached -m 256 -u root -p 12000 -d
/usr/bin/memcached -m 256 -u root -p 11211 -d
```
> 启动
```shell script
./memcached.sh start
```