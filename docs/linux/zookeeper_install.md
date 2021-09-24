- 下载zookeeper-3.4.9
```shell script
wget http://archive.apache.org/dist/zookeeper/zookeeper-3.4.9/zookeeper-3.4.9.tar.gz
```
- 解压zookeeper-3.4.9
```shell script
tar -zxvf zookeeper-3.4.9.tar.gz -C /usr/local/
```
- 在zookeeper-3.4.9中创建目录(根据自己zookeeper安装的路径进行修改路径)
```shell script
mkdir /usr/local/zookeeper-3.4.9/data
mkdir /usr/local/zookeeper-3.4.9/logs
```

- 复制`zoo_sample.cfg`文件,并对重命名后的文件`zoo.cfg`进行编辑(根据自己zookeeper安装的路径进行修改路径)
```shell script
cd /usr/local/zookeeper-3.4.9/conf
cp zoo_sample.cfg zoo.cfg
```

- 重命名
```shell script
mv zookeeper-3.4.9/ zookeeper
```
- 修改配置文件
```shell script
dataLogDir=/usr/local/zookeeper/logs
dataDir=/usr/local/zookeeper/data

#配置集群
server.1={pi}:2888:3888
```
- 编辑/etc/profile并在文件末尾添加zookeeper配置
```shell script
#编辑文件
vi /etc/profile 

#添加下面内容(根据自己的路径进行修改)
export ZOOKEEPER_HOME=/usr/local/zookeeper
export PATH=$ZOOKEEPER_HOME/bin:$PATH

#生效修改的配置
source /etc/profile
```
- 将zookeeper加入开机自启
```shell script
#编辑文件
vi /etc/init.d/zookeeper
```
>加入以下内容（根据自己的环境修改响应的路径）
[zookeeper](/conf/sh/zookeeper.sh.md)
```shell script
#给定执行权限并做成服务和加入开机自启
chmod a+x /etc/init.d/zookeeper
chkconfig zookeeper on
chkconfig --add zookeeper
```
- 相关命令
```shell script
service zookeeper start
service zookeeper stop
service zookeeper status
service zookeeper restart
```