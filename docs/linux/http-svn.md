### HTTP方式访问SVN配置

- 安装必要的rpm包
```shell script
yum install -y httpd subversion mod_dav_svn
```

- 创建SVN仓库
```shell script
mkdir -p /var/lib/svn
cd /var/lib/svn
svnadmin create sink
chown -R apache:apache sink
```

- 刷新目录下文件的权限：因为后续的httpd服务的用户默认为apache，
```shell script
chown -R apache:apache /data/svn/product_repo/
```

#### 调整SVN的配置文件
- cd到conf目录
```shell script
cd /data/svn/product_repo/conf/
```
- 用vim修改下server的配置
```shell script
vim svnserve.conf
```
> 修改文件svn配置，核心主要有以下几项：
```shell script
anon-access = none
auth-access = write
password-db = passwd
authz-db = authz
```

- 备份原来的账号密码配置文件
```shell script
mv passwd passwd.default
```
- htpasswd 接下来使用此命令创建新的账号密码文件，并往里面追加新的用户信息
> 创建passwd文件，添加用户zhangsan，密码为password
```shell script
htpasswd -cbm passwd zhangsan password
```
> 追加用户lisi，密码为1234
```shell script
htpasswd -bm passwd lisi 1234
```

#### 配置用户权限
- [参考文件auth](../conf/conf/auth)
```shell script
vim authz
```

- 最后，调整完配置的conf目录如下：
```base
├── authz
├── passwd
├── passwd.default
└── svnserve.conf
```
#### 配置httpd

- 创建配置文件 [参考文件svn.conf](../conf/conf/svn.conf)
```shell script
cd /etc/httpd/conf.d
touch svn.conf
vim svn.conf
```

- 修改监听端口
```shell script
vim /etc/httpd/conf/httpd.conf
Listen 4690
```

- 启动httpd服务
```shell script
systemctl enable httpd
systemctl start httpd
```