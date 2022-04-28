### redis安装
```
docker search redis 
docker pull redis:latest
docker run -d --name redis -p 6379:6379 redis:latest --requirepass "password"
```