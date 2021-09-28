### jenkins安装
> 提供了两种安装方式 可自行选择
- 安装
````shell script
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
yum install jenkins
````
- 配置
```shell script
#jdk配置
vim /etc/init.d/jenkins
在 candidates 后追加jdk 安装路径
/usr/local/java/jdk1.8.0_221/bin/java
```
-启动端口已经工作目录配置
> 可指定目录存放位置
```shell script
vim /etc/sysconfig/jenkins

JENKINS_HOME="/home/jenkins"

JENKINS_USER="root"

JENKINS_PORT="8588"
```
- 启动
```shell script
systemctl start  jenkins
```
- 访问
```shell script
#出现Please wait while Jenkins is getting ready to work
/var/lib/jenkins/hudson.model.UpdateCenter.xml
#https 修改为 http
```

### Jenkins安装
- rpm 包的下载
> 从官网上下载rpm的速度简直让人不能忍受，所以千万不要去官网下载。推荐去：http://mirrors.jenkins-ci.org/status.html 选择第一个清华大学的镜像站，再选择redhat，可以快速下载到最新的镜像。

- 安装 将rpm包上传至centos 中
```shell script
#1、执行 
rpm -ivh jenkins-2.183-1.1.noarch.rpm

#2、修改 用户名和端口 
vi /etc/sysconfig/jenkins
#修改：
JENKINS_USER = "root"
#修改：
JENKINS_PORT = "8588"

#3、配置jdk路径
vi /etc/init.d/jenkins
#在 candidates 后追加jdk 安装路径
/usr/local/bin/jdk1.8.0_162/bin/java #（一直到jdk安装路径下的bin/java）

systemctl daemon-reload
systemctl start jenkins
```

- 在浏览器访问ip:port 即可（在此之前需开放端口，如果是学习之用可关闭防火墙），如果此时提示 Please wait while Jenkins is getting ready to work，长时间没反应则
![](../images/jenkins/jenkins_use_1.png)
> 将 https://updates.jenkins.io/update-center.json 修改为 "http://mirror.xmission.com/jenkins/updates/update-center.json"

```shell script
vi /var/lib/jenkins/hudson.model.UpdateCenter.xml
systemctl daemon-reload #并重启服务
```

- 此时需要输入初始密码
![](../images/jenkins/jenkins_02.png)
> 里面的内容就是初始密码
```shell script
cat /var/lib/jenkins/secrets/initialAdminPassword
```
> 如果不习惯英文环境，可以安装 localization-zh-cn-plugin

- 卸载
```shell script
rpm -e jenkins      #卸载
rpm -ql jenkins     #检查是否卸载成功 
find / -iname jenkins | xargs -n 1000 rm -rf    #彻底删除残留文件
```
