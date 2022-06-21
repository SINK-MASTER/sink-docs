## GitLab


### 更新ssl证书

> 先准备好证书文件xx.crt、xx.key 
>
> 若证书为`.pem`直接更改为`.crt`

```sh
cd /etc/gitlab/
vim gitlab.rb 
```

```shell
external_url 'https://xxx.xxx'
nginx['ssl_certificate'] = "证书存放路径/xxx.com.crt"
nginx['ssl_certificate_key'] = "证书存放路径/xxx.com.key"
```


> 证书信息修改完毕后更新gitlab配置

```shell
gitlab-ctl reconfigure
```

> gitlab重新启动

```shell
gitlab-ctl restart
```

