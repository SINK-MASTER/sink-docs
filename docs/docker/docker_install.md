## 卸载旧版本
> 卸载老版本的 docker 及其相关依赖
```shell script
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

> - 安装yum-utils包（提供yum-config-manager 实用程序）并设置稳定的存储库。
```shell script
sudo yum install -y yum-utils
sudo yum-config-manager \
   --add-repo \
   https://download.docker.com/linux/centos/docker-ce.repo
```

## 卸载docker
> 卸载 Docker 引擎、CLI 和 Containerd 软件包：
```shell script
sudo yum remove docker-ce docker-ce-cli containerd.io
```
> 主机上的映像、容器、卷或自定义配置文件不会自动删除。要删除所有映像、容器和卷：
```shell script
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

## 启动 docker
```shell script
sudo systemctl start docker
```

## 其他
- 添加yum源
```shell script
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```
- 更新索引
```shell script
sudo yum makecache fast
```
- 安装 `docker-ce`
```shell script
sudo yum install docker-ce
```
-  验证是否安装成功
```shell script
sudo docker info
```
> 如果出现docker命令无法tab补全的问题
- 安装`bash-completion`
```shell script
yum install -y bash-completion
```
- 刷新文件
```shell script
source /usr/share/bash-completion/completions/docker
source /usr/share/bash-completion/bash_completion
```