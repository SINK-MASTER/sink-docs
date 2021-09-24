> nginx下载地址：https://nginx.org/download/
- 解压
```shell script
tar -zxvf nginx-1.9.9.tar.gz
```
- 安装
```shell script
cd nginx-1.9.9
./configure --prefix=/usr/local/nginx
```
> 出现问题
>`the HTTP rewrite module requires the PCRE library.`
```shell script
yum -y install pcre-devel
```

> 出现问题
> `the HTTP gzip module requires the zlib library.`
```shell script
yum install -y zlib-devel
```

- [配置nginx.conf](/conf/conf/nginx.conf.md)

- 启动
```shell script
/usr/local/nginx/sbin/nginx
```

- 重启
```base
/usr/local/nginx/sbin/nginx –s reload
```
- 停止
```base
/usr/local/nginx/sbin/nginx –s stop
```

- 测试配置文件是否正常
```base
/usr/local/nginx/sbin/nginx –t
```
- 强制关闭
```base
pkill nginx
```

- nginx配置文件
```based
/usr/local/nginx/conf/nginx.conf
```

- 脚本方式启动
> [启动文件](/conf/sh/nginx.sh.md)
- 创建文件
```shell script
cd /home
toucht nginx.sh
```
- 添加脚本内容
```shell script
vim nginx.sh
```

- 配置脚本权限
```shell script
chmod a+x /home/nginx.sh
```