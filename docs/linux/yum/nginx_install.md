## yum安装Nginx
- 安装
```shell script
yum -y install nginx
```
- 查看安装目录
> /etc/nginx
```shell script
rpm -ql nginx
```

- 相关操作
```shell script
systemctl start nginx
systemctl status nginx
systemctl restart nginx
systemctl stop nginx
systemctl enable nginx
```