### SVN仓库安装
- 安装SVN
```shell script
yum install -y httpd subversion mod_dav_svn #云命令安装
```
- 查看安装版本
```shell script
svnserve --version
```
- 创建版本库
```shell script
mkdir -p /var/lib/svn
cd /var/lib/svn
svnadmin create devops
chown -R apache:apache devops
```
- 目录说明
```
proname
|——conf #是这个仓库的配置文件（仓库的用户访问账号、权限等）
|   |——authz #权限控制文件
|   |——passwd #帐号密码文件
|   |——svnserve.conf #SVN服务配置文件
|——db #所有版本控制的数据存放文件
|——format #是一个文本文件，里面只放了一个整数，表示当前文件库配置的版本号
|——hooks #放置hook脚本文件的目录
|——locks #用来放置subversion见艰苦锁定数据的目录，用来追踪存取文件库的客户端
```
- 账户设置
```shell script
cd /conf
vim passwod
#输入账户 账号=密码
account=passwod

#设置权限
vim auth
#设置权限 账号=权限 r读w写
account=rw

#修改svnserve.conf文件 vi svnserve.conf
#打开下面的几个注释：

anon-access = read #匿名用户可读
auth-access = write #授权用户可写
password-db = passwd #使用哪个文件作为账号文件
authz-db = authz #使用哪个文件作为权限文件
realm =/var/svn/目录名 # 认证空间名，版本库所在目录
```

- 启动svn版本库
```shell script
svnserve -d -r /var/svn/repo --listen-port=3690
```
- 停止SVN
```shell script
killall svnserve
```
- 卸载SVN
```shell script
yum remove subversion
```