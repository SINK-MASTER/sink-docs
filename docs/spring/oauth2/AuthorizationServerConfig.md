## OAuth2 授权服务器配置

>###### 创建配置类 继承`AuthorizationServerConfigurerAdapter`

```java
@Configuration
@EnableAuthorizationServer
public class AuthorizationServerConfig extends AuthorizationServerConfigurerAdapter {
    
}
```

>###### 实现方法 configure(ClientDetailsServiceConfigurer clients)

```text
@Autowired
private DataSource dataSource;

@Override
public void configure(ClientDetailsServiceConfigurer clients) throws Exception {
    // 设置授权服务器配置信息从数据库中查询获取
    clients.withClientDetails(clientDetailsService());
}

public ClientDetailsService clientDetailsService() {
    return new JdbcClientDetailsService(dataSource);
}
```

>###### oauth_client_details

```sql
create table oauth_client_details (
  client_id VARCHAR(256) PRIMARY KEY,
  resource_ids VARCHAR(256),
  client_secret VARCHAR(256),
  scope VARCHAR(256),
  authorized_grant_types VARCHAR(256),
  web_server_redirect_uri VARCHAR(256),
  authorities VARCHAR(256),
  access_token_validity INTEGER,
  refresh_token_validity INTEGER,
  additional_information VARCHAR(4096),
  autoapprove VARCHAR(256)
);
```

| 参数名                  | 描述                                                         |
| ----------------------- | ------------------------------------------------------------ |
| client_id               | 授权服务器client-id，用于唯一标识每一个客户端                |
| resource_ids            | 客户端所能访问的资源id集合,多个资源时用逗号(,)分隔<br />Authorization Server给client第三方客户端授权的时候，可以设置这个client可以访问哪一些Resource Server资源服务，如果没设置，就是对所有的Resource Server都有访问权限。 |
| client_secret           | 加密后的client-secret，加密方式BCryptPasswordEncoder         |
| scope                   | 指定客户端申请的权限范围,可选值包括*read*,*write*,*trust*;若有多个权限范围用逗号(,)<br />@EnableGlobalMethodSecurity(prePostEnabled = true)启用方法级权限控制<br />配合注解@PreAuthorize(value = "#oauth2.hasScope('read')")使用 |
| authorized_grant_types  | 授权类型，可选值包括*authorization_code*,*password*,*refresh_token*,*implicit*,*client_credentials*, 若支持多个grant_type用逗号(,)分隔<br />最常用的grant_type组合有: "authorization_code,refresh_token"(针对通过浏览器访问的客户端); "password,refresh_token"(针对移动设备的客户端).<br/>在OAuth2.0 提供的地方进行扩展自定义的授权 |
| web_server_redirect_uri | 授权后重定向地址                                             |
| authorities             | 指定客户端所拥有的Spring Security的权限值,可选, 若有多个权限值,用逗号(,)分隔<br />配合注解@PreAuthorize(value = "hasAnyRole('ROLE_ADMIN')")使用 |
| access_token_validity   | token有效期（秒）<br />若不设定值则使用默认的有效时间值(60 * 60 * 12, 12小时) |
| refresh_token_validity  | refresh_token有效期（秒）<br />若不设定值则使用默认的有效时间值(60 * 60 * 24 * 30, 30天) |
| additional_information  | 这是一个预留的字段,在Oauth的流程中没有实际的使用,可选,但若设置值,必须是JSON格式的数据 |
| autoapprove             | 设置用户是否自动Approval操作, 默认值为 'false', 可选值包括 'true','false', 'read','write'.<br/>该字段只适用于grant_type="authorization_code"的情况,当用户登录成功后,若该值为'true'或支持的scope值,则会跳过用户Approve的页面, 直接授权. |

