## Docker 加速器配置
> 加速地址可在阿里云自行获取 `https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors`
```shell script
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
    "registry-mirrors": ["https://bpma5bzi.mirror.aliyuncs.com"],
    "insecure-registries": ["127.0.0.1:1180"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```
- 配置Docker加速器 [参考文件daemon.json ](conf/json/daemon.json.md)

- 这种写法是没有配置Docker加速器的情况下
> `单个私服的写法`
```json
{
    "insecure-registries": ["registry的IP地址:端口号"]
}
```
> `多个私服的写法`
```json
{
    "insecure-registries": ["registry1的IP地址:端口号","registry2的IP地址:端口号"]
}
```

- 这种写法是配置过Docker加速器的情况下  
> `单个私服的写法`
```json
{
    "registry-mirrors": ["http://f1361db2.m.daocloud.io"],
    "insecure-registries": ["registry的IP地址:端口号"]
}
```
> `多个私服的写法`
```json
{
    "registry-mirrors": ["http://f1361db2.m.daocloud.io"],
    "insecure-registries": ["registry1的IP地址:端口号","registry2的IP地址:端口号"]
}
```