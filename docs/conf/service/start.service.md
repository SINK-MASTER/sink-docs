```text
[Unit]
Description=system self start service # 描述
[Service]
WorkingDirectory=/home/sink/workspace/ #项目目录
PrivateTmp=true
Restart=always
Type=simple
# 启动目录 使用绝对路径 jdk路径 -jar -D参数名=参数值 jar包绝对路径
ExecStart=/usr/local/java/jdk1.8.0_171/bin/java -jar -Dmysqlserver=127.0.0.1:3306 /home/ezz/ccb/ccb-web-app-1.0.0.0-SNAPSHOT.jar &
ExecStop=/usr/bin/kill -15 $MAINPID

[Install]
WantedBy=multi-user.target
~
```