## OAuth2.0授权模式

### 授权码模式

###### 一、获取code

------

1.1.获取URL：

> http://localhost:8080/oauth/authorize?response_type=code&client_id={clientId}&redirect_uri={redirect_uri}&scope=all&state={state}

1.2.请求方式:

> GET



| 参数名        | 参数值 | 是否必须 | 类型   | 描述                                                       |
| ------------- | ------ | -------- | ------ | ---------------------------------------------------------- |
| client_id     |        | 是       | string | 应用ID                                                     |
| redirect_uri  |        | 是       | string | 回跳地址(必需和应用配置里面的地址一致)                     |
| response_type | code   | 是       | string | 返回类型                                                   |
| scope         |        | 是       | string | 授权范围                                                   |
| state         |        | 否       | string | 表示客户端的当前状态，可以指定任意值，认证服务器会原样返回 |

###### 二、通过code获取token

------

2.1.请求地址

>http://localhost:8080/oauth/token?code={code}&grant_type={grant_type}&redirect_uri={redirect_uri}&scpoe={scpoe}

2.2.请求方式

> POST

2.3.请求头

| 参数名        | 参数值                          | 是否必须 | 类型   | 描述                                                         |
| ------------- | ------------------------------- | -------- | ------ | ------------------------------------------------------------ |
| Authorization | Basic {clientId}:{clientSecret} | 是       | string | {clientId}:{clientSecret} 的值必需使用base64加密，clientId为应用id，clientSecret为应用密钥 |

2.4.请求参数

| 参数名       | 参数值             | 是否必须 | 类型   | 描述                 |
| ------------ | ------------------ | -------- | ------ | -------------------- |
| code         |                    | 是       | string | 授权码               |
| grant_type   | authorization_code | 是       | string | 授权类型             |
| redirect_uri |                    | 是       | string | 授权重定向地址       |
| scope        |                    | 是       | string | 客户端申请的权限范围 |



### 密码授权模式

###### 一、获取token

------

1.1.请求URL

>http://localhost:8080/oauth/token?grant_type=password&username={username}&password={password}&account_type={account_type}

1.2.请求方式

> POST

1.3.请求头

| 参数名        | 参数值                          | 是否必须 | 类型   | 说明                                                         |
| :------------ | :------------------------------ | :------- | :----- | :----------------------------------------------------------- |
| Authorization | Basic {clientId}:{clientSecret} | 是       | string | {clientId}:{clientSecret} 的值必需使用base64加密，clientId为应用id，clientSecret为应用密钥 |

1.4.请求参数

| 参数名       | 参数值   | 是否必须 | 类型   | 描述     |
| ------------ | -------- | -------- | ------ | -------- |
| grant_type   | password | 是       | string | 授权类型 |
| username     |          | 是       | string | 用户名   |
| password     |          | 是       | string | 密码     |
| account_type |          | 是       | string | 用户类型 |



### 简化模式授权

###### 一、获取token

------

1.1.请求URL

> http://localhost:9900/api-uaa/oauth/authorize?client_id={client_id}&redirect_uri={redirect_uri}&response_type=token&scope={scope}

 1.2.请求方式

> GET

1.3.请求参数

| 参数名        | 参数值 | 是否必须 | 类型   | 说明     |
| :------------ | :----- | :------- | :----- | :------- |
| client_id     |        | 是       | string | 应用id   |
| redirect_uri  |        | 是       | string | 回调地址 |
| response_type | token  | 是       | string | 返回类型 |
| scope         |        | 否       | string | 授权范围 |

1.4.返回

> 登录成功后跳转回调地址并带上token参数



### 客户端模式授权

###### 一、 获取token

------

###### 1.1.请求URL

> http://localhost:9900/api-uaa/oauth/token?grant_type=client_credentials

1.2.请求方式

> POST

1.3.请求头

| 参数名        | 参数值                          | 是否必须 | 类型   | 说明                                                         |
| :------------ | :------------------------------ | :------- | :----- | :----------------------------------------------------------- |
| Authorization | Basic {clientId}:{clientSecret} | 是       | string | {clientId}:{clientSecret} 的值必需使用base64加密，clientId为应用id，clientSecret为应用密钥 |

1.4.请求参数

| 参数名     | 参数值             | 是否必须 | 类型   | 说明     |
| :--------- | :----------------- | :------- | :----- | :------- |
| grant_type | client_credentials | 是       | string | 授权类型 |