- 拉取镜像
```shell script
docker pull jenkins/jenkins:2.313
```
- 启动
```shell script
docker run \
-d \
-u root \
--name=jenkins \
-v /home/docker/jenkins/jenkins_home:/var/jenkins_home \
-p 8006:8080 \
-p 8007:5000 \
jenkins/jenkins:2.313
```

- 查看日志
```shell script
docker logs -f ${CONTAINER_ID}
```
![](../images/jenkins/jenkins_01.png)

> `复制密码并输入`  

![](../images/jenkins/jenkins_02.png)

- 选择安装方式

![](../images/jenkins/jenkins_03.png)

- 等待安装

![](../images/jenkins/jenkins_04.png)

- 设置密码

![](../images/jenkins/jenkins_07.png)
- 实例配置

![](../images/jenkins/jenkins_08.png)
- 进入主页

![](../images/jenkins/jenkins_06.png)


- 问题
> 进入首页一直处于 `Please wait while Jenkins is getting ready to work ...`  
> 修改 `/home/docker/jenkins/jenkins_home`下`hudson.model.UpdateCenter.xml`中  
> `https://updates.jenkins.io/update-center.json` 
>  更改为国内镜像地址 `https://mirrors.tuna.tsinghua.edu.cn/jenkins/updates/update-center.json`

![](../images/jenkins/jenkins_05.png)
