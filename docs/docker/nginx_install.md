-拉取镜像
```shell script
docker pull nginx:latest
```

-启动nginx
```shell script
docker run \
--name=nginx \
-d \
-p 80:80 \
-v /home/docker/nginx/:/etc/nginx/ \
nginx:latest
```

-设置登陆验证
> 进入容器
```shell script
docker exec -it ${CONTAINER_ID} /bin/bash
```

> 下载apache2-utils
```shell script
apt-get update
apt-get install apach2-utils
```

> 添加登陆账号
```shell script
htpasswd -c /etc/nginx/password ${USER_NAME}
```

> 进入conf文件添加一下配置
```shell script
auth_basic "login prompt"; #这里是验证时的提示信息
auth_basic_user_file /etc/nginx/passwd;
```