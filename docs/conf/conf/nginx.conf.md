```text
# 工作进程数 默认 1 CPU核心数，(双核4线程，可以设置为4)
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

worker_rlimit_nofile 100000;
events {
    # 单个工作进程可以允许同时建立外部连接的数量
    worker_connections  1024;
	multi_accept on;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr $request_body - $remote_user [$time_local] "$request" '
                          '$status $body_bytes_sent "$http_referer" '
                          '"$http_user_agent" "$http_x_forwarded_for" '
                          '$request_time $upstream_response_time ';

    limit_req_zone $binary_remote_addr zone=one:50m rate=20r/s;
    limit_conn_zone $binary_remote_addr zone=addr:50m;

    log_format access '$remote_addr - $remote_user [$time_local] "$request" $status $body_bytes_sent $request_body "$http_referer" "$http_user_agent" $http_x_forwarded_for';
    access_log  /usr/local/nginx/logs/access.log access;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  965;

    ## 配置单独隔离，各个项目配置单独创建 统一引入
    include /etc/nginx/sink/*.conf;
}
```