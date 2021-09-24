- 下载完成后解压至安装路径
       
- 设置访问端口
````shell script
/usr/local/nexus-2.5.0-04/conf
application-port=8888
````
```shell script
#nexus
export RUN_AS_USER=root
source /etc/profile
```
- 启动
```shell script
./nexux start
```

- 配置
```
进入仓库管理页面登录后找到Central
1、设置Remote Storage Location
http://maven.aliyun.com/nexus/content/groups/public/
2、Download Remote Indexes
设置为true保存即可
```

- 问题
> Error in WrapperListener.start callback.  java.lang.StackOverflowError
> 上面这种问题为使用的jdk版本不兼容
> nexus version: 2.5.0-04
> 指定jdk版本: 1.7
```shell script
cd /usr/local/nexus-2.5.0-04/bin/jsw/conf
vim wrapper.conf
```
> 修改如下配置
```shell script
#wrapper.java.command=java
wrapper.java.command=/usr/local/java/jdk1.7.0_80/bin/java
```