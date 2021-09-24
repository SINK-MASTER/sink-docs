### 安装
> 1、下载与解压
```shell script
wget https://dlcdn.apache.org/lucene/solr/7.7.3/solr-7.7.3.tgz

tar -zxvf solr-7.7.3.tgz
```
> 文件目录
![](../images/solr/solr_1.png)

### 配置
> 1、自定义core名称 `core_name`
```shell script
./bin/solr create -c core_name
```
> 2、配置文件修改
> 1. [修改solrconfig](/conf/solr/solrconfig.md) 添加引入jar位置与自定义jdbc
> 2. [添加data-config.xml](/conf/solr/data-config.md) 创建`data-config.xml`至`/server/solr/answer_problem/conf`
> 3. [修改managed-schema](/conf/solr/managed-schema.md) 修改主键
> 4. [修改solr.in.sh](/conf/solr/solr.in.sh.md) 修改市区

### 命令
```shell script
./bin/solr start    启动
./bin/solr stop     停止
./bin/solr resatrt  重启  
```