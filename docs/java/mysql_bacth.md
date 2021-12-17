> Mysql批量导入 数据插入过慢问题解决

> Mysql使用`SqlSessionTemplate`批量导入数据时在
>`jdbc`配置需要追加`rewriteBatchedStatements=true`否则不会生效

```yaml
spring:
  main:
    allow-bean-definition-overriding: true
  datasource:
    url: jdbc:mysql://127.0.0.1:3306/jhsh?useUnicode=true&characterEncoding=utf8&autoReconnect=true&characterSetResults=utf8&allowMultiQueries=true&useSSL=false&rewriteBatchedStatements=true
    username: root
    password: root
```

> 在配合SqlSessionTemplate使用
```text
SqlSessionFactory sessionFactory = sqlSessionTemplate.getSqlSessionFactory();
sessionFactory sqlSession = sessionFactory.openSession(ExecutorType.BATCH);
sqlSession.insert("com.sink.xxx.insertDao.inertMethod", paramVO);
```