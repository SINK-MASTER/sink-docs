-Linux下自启动服务
> 编写脚本文件参考[start.service](/conf/service/start.service.md)

-命令
```shell script
systemctl statr start.service
systemctl stop start.service
```

-加入自启动
```shell script
systemctl enable start.service
```