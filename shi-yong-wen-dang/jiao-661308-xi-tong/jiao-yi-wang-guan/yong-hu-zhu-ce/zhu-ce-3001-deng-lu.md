### 一、用户注册、登录

#### 1.查看注册类型

```
GET    http://localhost:8082/auth/user/activationType
```

* **返回参数说明：**

  * **key 时，使用邮件验证码激活。注册需要传入 activated 值，使用邮件验证码激活逻辑。（业务层创建账户时，自动创建底层交易账户）**

  * **link 时，使用邮件链接激活。（业务层账户激活成功，创建底层交易账户）**

* **返回结果：**

```
key / link
```

#### 2.检查Email（Mobile）是否可以注册（权限开放）

```
GET    http://localhost:8082/auth/user/login/check/{login}
```

* String **login : 支持邮箱、手机**
* **返回结果：true 已经存在，不能注册，false 可以注册**

```
true / false
```

* **异常情况：**
  * **404  邮件格式不正确**
  * **410 多账号绑定同一手机号，不支持检查**

#### 3.使用 Email（Mobile） 注册用户 （权限开放）

```
POST    http://localhost:8082/auth/user/register
```

* **接口使用说明：（手机注册只支持 KEY 激活方式）**
  * **手机注册只支持激活方式为 key，因为无法发送激活邮件链接。**
  * **Gateway 和 UAA 的配置必须保持一致**
  * **activationType 为 key 时，使用邮件验证码激活逻辑。（业务层创建账户时，自动创建底层交易账户）**
  * **activationType 为 link 时，使用邮件激活链接激活逻辑。（业务层账户激活成功，创建底层交易账户）**

```
Gateway 注册配置：
application:
    uaa:
        activationType: key # link key

UAA 注册配置：
application:
    registerConfig:
        activationType: key # link key
        passwordLength: # password 密码长度配置
            min: 9
            max: 16
        currencyPasswordLength: # 资金密码长度配置
            min: 6
            max: 16
```

* **账户流程：**

![](/assets/用户注册流程图.png)

```
用户通过 Gateway网关注册，UAA 用户中心会读取 Git 配置中心，根据注册方式是 Key 还是 Link 进行不同处理。
1．注册方式是Key，业务层用户直接激活。在返回数据时，被Gateway网关的后置过滤器 CreateUserFilter 拦截，创建底层账户，
调用邮件服务发送欢迎邮件。如果底层服务挂掉，则提示用户异常，联系网站修复账户的完整性。
2．注册方式是Link，用户未激活状态，并设置 ActivationKey。在返回数据时，被Gateway网关的后置过滤器 CreateUserFilter 拦截，
调用邮件服务发送激活链接邮件（发送邮件前Gateway网关会请求 UAA 服务获取当前用户的 ActivationKey 设置到邮件链接内），
当用户点击邮件链接激活业务层用户后，被Gateway网关的后置过滤器 ActivateUserFilter拦截，创建底层账户，
再次调用邮件服务发送欢迎邮件。如果底层服务挂掉，则提示用户异常，联系网站修复账户的完整性。
```

* **参数说明：**
  * String **email : 支持 a\_b-.@x-y.com 类似格式**
  * String **password : 长度可配置**
  * Boolean **actived : 该字段根据 activationType 值决定是否传入， true \[ 用户邮箱已验证 \]  （如果为 false ，用户未激活，3天后自动删除账号）**
  * String **password : 密码必须使用 **_**sun.misc.BASE64Encoder**_** 的 base64 进行编码 **

```
{  
 "email":"admin@localhost.com", 
 ["mobile":"+86-13800001234",]
 "password":"YWRtaW4uYWRtaW4=", 
 ["activated":true,]
 "langKey":"zh-CN" 
}
```

* **返回参数说明：**
  * REGISTER\_SUCCESS  **注册成功且已激活（业务层账户、底层交易账户同时注册成功）**
  * REGISTER\_NOT\_ACTIVATE **注册成功，未激活（业务层账户注册成功，需要激活业务层账户，此时底层账户在用户激活业务成账户后创建）**
  * REGISTER\_FAILED **注册成功，底层账户创建失败（需要提醒用户联系网站管理员修复账号）**
  * REGISTER\_EXCEPTION** 注册异常（网站配置问题，提示用户联系网站）**
* **返回结果：**

```
“REGISTER_SUCCESS”
```

* **异常情况：**
  * **500  邮箱已存在、密码长度不符合规则**
  * **410  手机号已绑定多个账户，不允许注册**

#### 4.用户点击邮件内的 Link 激活（权限开放，activationType 配置为 link 时启用该加密接口）

```
GET    https://localhost:8080/auth/user/activate?key={key}
```

* **参数说明：**
  * String **key  （20 位激活码）**
* **返回参数说明：**

  * REGISTER\_SUCCESS  **注册成功且已激活（业务层账户、底层交易账户同时注册成功）**

  * REGISTER\_FAILED **注册成功，底层账户创建失败（需要提醒用户联系网站管理员修复账号）**

  * REGISTER\_EXCEPTION** 注册异常（网站配置问题，提示用户联系网站）**

* **返回结果：**

```
“REGISTER_SUCCESS”
```

* **异常情况：500 激活 Key 不存在**

#### 5.使用 Email（手机号）、密码鉴权获取登录状态（权限开放）

```
POST    http://localhost:8082/auth/user/login/status
```

* **接口使用方法：（/login/status 之后选择用户校验方式步骤省略）**
  * **邮箱登录：调用 /check/email 接口检测该邮箱是否存在，然后调用 /login/status 获取用户状态，最后调用 /login 接口。**
  * **手机登录：调用 /bind/info 接口检测该手机号是否绑定，然后调用 /login/status 获取用户状态，最后调用 /login 接口。**
* **接口流程：（不会有 Token 种入 Cookie）**
* **配置说明：**
  * **如果 gateway.yml 配置登录限制，则显示下列数据**
  * **如果未配置限制，则只有 status 状态**
* **返回 status 说明：**
  * **NORMAL  允许登录（业务层账户正常）**
  * **FREEZE  禁止登录（业务层账户被冻结）**
  * **LIMIT  提示用户超过限制次数，在限制时间后登录**
  * **EXCEPTION  用户名或密码错误，重新登录**
  * **NOT\_ACTIVATED  当前用户未激活，提示用户激活该账户（activationTye 为 link 时会有该返回值）**

```
         Right |---> NORMAL { "dayLimit": 10, "status": "NORMAL" }
       |------>|
       |       |---> FREEZE { "dayLimit": 10, "status": "FREEZE" }
       |       |
Web -->|       | 
       | Wrong |                   |--> { "dayLimit": 10, "dayExpire": 600, "dayUsedLimit": 0, "status": "EXCEPTION" }
       |       |---> EXCEPTION --> |
       |       |                   |--> { "dayLimit": 10, "dayExpire": 600, "dayUsedLimit": 0, "status": "MULTI_ACCOUNT" }
       |       |                   |  
       |----- >|                   |--> { "dayLimit": 10, "dayExpire": 600, "dayUsedLimit": 0, "status": "NOT_ACTIVATED" }
               |
               |---> LIMIT { "dayLimit": 10, "dayExpire": 390, "dayUsedLimit": 10, "status": "LIMIT" }
```

* **参数：**

```
{
  "username":"32694110@qq.com",
  "password":"YWRtaW4uYWRtaW4="
}
```

* **返回结果：**

```
{
  "dayLimit": 10,
  "dayExpire": 600,
  "dayUsedLimit": 0,
  "status": "EXCEPTION"
}
```

* **异常情况：无**

#### 6.使用 Email（Mobile）、密码鉴权登录（权限开放）

```
POST    http://localhost:8082/auth/user/login
```

* **接口说明：**

  * **首先调用 /auth/user/login/status 获取用户状态为 NORMAL 时，然后调用 /auth/user/bind/info/{login} 获取用户绑定状态，校验完成后，调用该接口，然后再调用 /auth/user/login-callback 记录用户 IP。**

  * **主要防止用户过早获取 token ，跳过验证过程。**

* **接口流程：**

```
   A  获取登录状态
   |                       获取绑定状态          
   |              1.                 
   |             |------------------------------------| 
  \|/            |2.                                  |
  NORMAL ----> B |---------------> D ---> (true) -----|  登录
                 |3.                                  |------> C  
                 |---------------> E ---> (true) -----|        |
                 |4.                                  |        |
                 |---------------> D/E -> (true) -----|        |
                                                              \|/

                                                               G 记录用户登录历史（Gateway Filter）

  A:auth/user/login/status
  B:auth/user/bind/info/{login}
  C:auth/user/login
  D:security/sms/send/{mobile}/{type}
  E:auth/user/bind/g-auth/verify/{login}/{gaCode}
  F:security/sms/verify/{type}/{mobile}/{code}
  G:auth/user/records-address

  1:没有绑定手机
  2:绑定手机
  3:绑定 GA                         
  4:绑定手机、GA
```

* **参数说明：**
  * String **username : 如果手机号登录需要注意固定格式**
  * Boolean **rememberMe :  true \(默认Token 保存7天 \) / false \(默认Token 保存30分钟\)**

```
{
   "username":"32694110@qq.com",
   "password":"YWRtaW4uYWRtaW4=",
   "rememberMe":"true"
}
```

* **返回结果：**

```
true
```

* **异常情况：500  用户名或密码错误**

#### 7.用户登录，并记录历史

```
GET    http://localhost:8082/auth/user/login-callback
```

* **接口说明：**

  * **用户登录调用，记录用户的 IP 信息，禁止别的地方调用。**
  * **当查询用户 IP 状态成功且用户绑定手机时，会发送登录短信。**

* **返回结果：**

```
{
  "id": 3,
  "email": "admin@localhost.com",
  "mobile": "+86-10010",
  "inkId": "1010",
  "areaCode": "+86",
  "firstName": "Administrator",
  "lastName": "Administrator",
  "imageUrl": "",
  "activated": true,
  "langKey": "en",
  "createdBy": "system",
  "createdDate": "2018-06-20T02:38:19Z",
  "lastModifiedBy": "system",
  "lastModifiedDate": null,
  "authorities": [
    "ROLE_USER",
    "ROLE_ADMIN"
  ]
}
```

* **异常情况：401  当前用户没有登录，调用该接口（正常逻辑不会出现）**

#### 8.查看用户信息（个人中心-基本信息 页面显示邮箱、手机号）

```
GET    http://localhost:8082/auth/user/info
```

* **返回结果：**

```
{
  "id": 3,
  "email": "admin@localhost.com",
  "mobile": "+86-10010",
  "inkId": "1010",
  "areaCode": "+86",
  "firstName": "Administrator",
  "lastName": "Administrator",
  "imageUrl": "",
  "activated": true,
  "langKey": "en",
  "createdBy": "system",
  "createdDate": "2018-06-20T02:38:19Z",
  "lastModifiedBy": "system",
  "lastModifiedDate": null,
  "authorities": [
    "ROLE_USER",
    "ROLE_ADMIN"
  ]
}
```

* **异常情况：401  当前用户没有登录，调用该接口（正常逻辑不会出现）**



