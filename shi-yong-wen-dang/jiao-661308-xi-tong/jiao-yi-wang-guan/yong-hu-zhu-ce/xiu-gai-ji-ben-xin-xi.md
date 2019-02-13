### 二、修改基本信息

#### 1.绑定、更新手机号码

```
POST    http://localhost:8082/auth/user/info
```

* **参数：**只有 String **mobile **是必传参数，其他的可以根据后期网站实际需求传值

```
{    
  "firstName": "string",   
  "imageUrl": "string",   
  "langKey": "string",            
  "lastName": "string",   
  "mobile": "string",           [ +86-138******** ]   
  "email" : "admin@admin.com",
  "areaCode": "string"          [ +86 ]   
}
```

* **返回结果：**

```
{
  "id": 3,
  "email": "admin@localhost.com",
  "mobile": "+86-13888888888",
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

* **异常情况：**

  * **400  用户绑定手机时，手机号码已经存在**

  * **410 多账号绑定同一手机号，不支持更新**

  * **500 当前用户没有登录，调用该接口（正常逻辑不会出现）**

#### 2.修改登录密码

```
PUT    http://localhost:8082/auth/user/change-pass
```

* **参数：**

```
{
  "oldPass":"123456789",
  "newPass":"abcdefghi"
}
```

* **返回结果：**

```
true / false
```

* **异常情况：**

  * **400 密码不符合长度规则**

  * **500 当前用户没有登录，调用该接口（正常逻辑不会出现）**

#### 3.重置登录密码 （权限开放）

```
POST    http://localhost:8082/auth/user/reset-pass
```

* **参数说明：**
  * **String login : 支持邮箱、手机**

```
{
  "pass":"123456789",
  "login":"admin@localhost.com"
}
```

* **返回结果：true 密码修改正确，false 新密码和旧密码相同，未修改成功**

```
true / false
```

* **异常情况：**

  * **400 密码不符合长度规则、传入邮件格式不对**
  * **410 多账号绑定同一手机号，不支持重置密码**

#### 4.用户登录历史

```
GET    http://localhost:8082/auth/user/login-logs
```

* **接口说明：默认只返回最近10条数据**

* **返回结果：**

```
[
  {
    "id": 420,
    "userId": 5,
    "ipAddress": "61.50.105.122",
    "countryName": "China",
    "cityName": "Beijing",
    "status": "success",
    "device": "PC",
    "createdBy": "10089",
    "createdDate": "2018-10-18T08:31:21Z",
    "lastModifiedBy": "10089",
    "lastModifiedDate": "2018-10-18T08:31:21Z"
  },
  {
    "id": 419,
    "userId": 5,
    "ipAddress": "61.50.105.122",
    "countryName": "China",
    "cityName": "Beijing",
    "status": "success",
    "device": "PC",
    "createdBy": "10089",
    "createdDate": "2018-10-18T08:13:49Z",
    "lastModifiedBy": "10089",
    "lastModifiedDate": "2018-10-18T08:13:49Z"
  },
  ......
]
```

* **异常情况：500 当前用户没有登录，调用该接口（正常逻辑不会出现）**

---

#### 验证级别 -- 参数说明：

```
loginType
                       0 use default strategy
                       1 use only password
                       2 use password + sms
                       3 use password + GA
                       4 use password + sms +GA

param currencyType
                       0 use default strategy
                       1 use only currencyPassword
                       2 use currencyPassword + sms
                       3 use currencyPassword + GA
                       4 use currencyPassword + sms + GA
```

#### 5.获取用户验证级别 \[ 暂未使用该功能 \]

```
GET    http://localhost:8082/auth/user/auth-type
```

* **返回结果：**

```
{
  "id": 4,
  "userId": 3,
  "loginType": 1,
  "currencyType": 1,
  "description": null,
  "extension": null,
  "createdBy": "1010",
  "createdDate": "2018-08-23T03:25:32Z",
  "lastModifiedBy": "1010",
  "lastModifiedDate": "2018-08-23T03:25:32Z"
}
```

* **异常情况：500 当前用户没有登录，调用该接口（正常逻辑不会出现）**

#### 6.设置用户验证级别 \[ 暂未使用该功能 \]

```
GET    http://localhost:8082/auth/user/auth-type/{loginType}/{currencyType}
```

* **参数说明：**
  * String  **loginType**
  * String  **currencyType**
* **返回结果：**

```
{
  "id": 4,
  "userId": 3,
  "loginType": 1,
  "currencyType": 1,
  "description": null,
  "extension": null,
  "createdBy": "1010",
  "createdDate": "2018-08-23T03:25:31.608Z",
  "lastModifiedBy": "1010",
  "lastModifiedDate": "2018-08-23T03:25:31.608Z"
}
```

* **异常情况：500 当前用户没有登录，调用该接口（正常逻辑不会出现）**

#### 7.记录用户登录 IP 地址（Gateway Filter 内部调用）

```
POST    http://localhost:8082/auth/user/records-address
```

* **接口说明：**默认自动在 login-callback 接口自动调用。
* **异常情况：500 当前用户没有登录，调用该接口（正常逻辑不会出现）**

#### 8.根据 Token 内的 Principal （coreId）获取用户信息（服务间内部加密调用）

```
GET    http://localhost:8082/auth/user/principal/{principal}
```

* **场景说明：**
  * **已登录用户，在后台被冻结后，调用其他接口，需要使用该接口确定最新的用户权限。**
* **返回结果：**
  * **同 user/info **



