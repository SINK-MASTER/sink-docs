- 安装包下载
> 目录地址 /etc/httpd
```shell script
yum install httpd
```

- 端口修改
> `80 -> 4690` 用于http方式访问svn
```shell script
cd /etc/httpd/conf
vim httpd.conf
```
- 命令
```shell script
systemctl start httpd.service
systemctl stop httpd.service
systemctl restart httpd.service
```

- 访问
> `http://ip:4690/`