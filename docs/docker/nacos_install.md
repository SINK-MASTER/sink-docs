- `注意修改配置文件，添加nacos.sql 数据持久化，否则重启后配置文件数据将丢失`
- 下载
> https://github.com/alibaba/nacos/releases

- 解压
```
unzip nacos-server-1.3.2.zip
```

- 启动
> 默认端口 8848
> 单机模式
```shell script
sh bin/startup.sh -m standalone
```
> http://localhost:8848/nacos/index.html#/login


## Spring Boot 配置Nacos
> 添加依赖
```
<!-- Nacos配置 -->
<dependency>
    <groupId>com.alibaba.boot</groupId>
    <artifactId>nacos-config-spring-boot-starter</artifactId>
    <version>${nacos.starter.version}</version>
</dependency>
<dependency>
    <groupId>com.alibaba.nacos</groupId>
    <artifactId>nacos-api</artifactId>
    <version>${nacos.api.version}</version>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>

    <exclusions>
        <exclusion>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
        </exclusion>
        <exclusion>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-core</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```
>修改配置文件
```yaml
spring:
  cloud:
    nacos:
      config:
        server-addr: 112.124.13.157:8848 # Nacos配置地址
        file-extension: yaml # 配置文件类型
        namespace: dbfaacb9-2b30-4567-9153-480ff87825c1 # 分组ID
  profiles:
    active: ${activeTag} # 动态配置分组名称 prod、test、dev
  application:
    name: sink-query # 配置文件名称
  main:
    allow-bean-definition-overriding: true
```