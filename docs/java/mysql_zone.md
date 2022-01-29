## Mysql时区问题

> com.mysql.cj.jdbc.Driver驱动  
> db保存`new Date()`日期数据时所获的的时区不对  
> 在数据库连接地址上添加`serverTimezone=Asia/Shanghai`