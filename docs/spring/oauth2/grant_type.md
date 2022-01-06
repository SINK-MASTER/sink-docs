## OAuth2.0授权模式



#### 授权码模式

> 获取code
>
> 请求方式：GET、POST
>
> 请求地址：http://localhost:8080/oauth/authorize?response_type=code&client_id=clientId&redirect_uri=http://localhost:8080&scope=all

| 参数          | 描述                 |
| ------------- | -------------------- |
| response_type | 授权类型             |
| client_id     | 授权服务器client-id  |
| redirect_uri  | 授权重定向地址       |
| scope         | 客户端申请的权限范围 |

> 授权码模式token获取
>
> 请求方式：POST
>
> Content-Type：application/x-www-form-urlencoded
>
> Headres：Authorization Basic `new Base64Encoder().encode('clientId:clientSecret')`
>
> 请求地址：http://localhost:8080/oauth/token

| 参数         | 描述                 |
| ------------ | -------------------- |
| code         | 授权码               |
| grant_type   | 授权类型             |
| redirect_uri | 授权重定向地址       |
| scope        | 客户端申请的权限范围 |

