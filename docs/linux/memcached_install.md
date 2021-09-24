- memcached依赖于libevent库,因此需要先安装 libevent
```shell script
wget https://github.com/libevent/libevent/releases/download/release-2.1.8-stable/libevent-2.1.8-stable.tar.gz

wget http://www.memcached.org/files/memcached-1.5.10.tar.gz
```
- 安装libevent
```shell script
tar zxvf libevent-2.0.21-stable.tar.gz

cd libevent-2.0.21-stable

./configure --prefix=/usr/local/libevent

make && make install
```
- 安装memcached
```shell script
tar zxvf memcached-1.4.5.tag.gz

cd memcached-1.4.5

./configure --prefix=/usr/local/memcached --with-libevent=/usr/local/libevent

make && make install
```
- 启动memcached
```shell script
memcached/bin/memcached -m 256 -u root -p 12000 -d
memcached/bin/memcached -m 256 -u root -p 11211 -d
```