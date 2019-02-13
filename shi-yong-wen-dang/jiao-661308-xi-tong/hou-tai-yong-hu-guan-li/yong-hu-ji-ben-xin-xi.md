#### 1.创建账户

```
POST    http://localhost:8080/manager/users/initial
```

* **接口说明：该接口只允许 ROLE\_ADMIN 权限的用户初始化一个管理后台账户。密码一般默认使用 login 。（没有邮件通知）**
* **参数说明：**
  * activated : 默认激活
  * email : 不允许重复
  * login : 不允许重复 
  * role : 不允许重复，业务层角色

```
{
  "activated": true,
  "email": "bonismo@hotmail.com",
  "langKey": "zh-CN",
  "login": "bonismo",
  "password": "admin",
  "role": "USER"
}
```

* **返回结果：**

```
{
  "id": 12,
  "login": "bonismo",
  "firstName": null,
  "lastName": null,
  "email": "bonismo@hotmail.com",
  "activated": true,
  "langKey": "zh-CN",
  "imageUrl": null,
  "role": "USER",
  "resetDate": null
}
```

* **异常情况：**400  login、email 已经存在

#### 2.用户登录（权限开放）

```
POST    http://localhost:8080/manager/authenticate
```

* **参数说明：**

```
{
  "password": "admin",
  "rememberMe": true,
  "username": "admin"
}
```

* **返回结果：**

```
{
  "id_token": "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJhZG1pbiIsImF1dGgiOiJST0xFX0FETUlOLFJPTEVfVVNFUiIsImV4cCI6MTU0NTc4Nzc3NX0.t_kfkvpUzbfQxeyqzGIhsc9IuFgBvRF5Vk30-NEk4R6M6oBlxXyVmRJUtuxc0imwbs1rSINiwe5TiDQlRj-RmQ"
}
```

* **异常情况：**401 用户或密码错误

#### 3.登录回调接口

```
GET    http://localhost:8080/manager/account-callback
```

* **返回结果：**

```
{
  "id": 3,
  "login": "admin",
  "firstName": "admin",
  "lastName": "",
  "email": "bonismo1@hotmail.com",
  "imageUrl": "string",
  "activated": true,
  "langKey": "zh-cn",
  "role": "ADMIN",
  "createdBy": "system",
  "createdDate": "2018-11-23T03:19:29Z",
  "lastModifiedBy": "admin",
  "lastModifiedDate": "2018-11-26T10:03:45.593Z",
  "authorities": [
    "ROLE_USER",
    "ROLE_ADMIN"
  ]
}
```

* **异常情况：500 未登录调用**

#### 4.获取当前登录用户（权限开放）

```
GET    http://localhost:8080/manager/authenticate
```

* **返回结果：如果有值则证明用户当前处于登录状态，如果无值，则未登录。**

```
admin
```

#### 5.更新用户信息（ROLE\_ADMIN 权限）

```
PUT    http://localhost:8080/manager/users
```

* **接口说明：由 ROLE\_ADMIN 权限修改其他用户的角色或者权限，及基本信息**
* **参数说明：**

```
{
  "id": 14,
  "login": "bonismo",
  "firstName": null,
  "lastName": null,
  "email": "bonismo@hotmail.com",
  "langKey": "zh-CN",
  "imgUrl":null,
  "activated":true,
  "role": "ADMIN"
}
```

* **返回结果：**如果更新的用户ID不存在，ResponseCode 404

```
{
  "id": 14,
  "login": "bonismo",
  "firstName": null,
  "lastName": null,
  "email": "bonismo@hotmail.com",
  "imageUrl": null,
  "activated": true,
  "langKey": "zh-CN",
  "role": "USER",
  "createdBy": "admin",
  "createdDate": "2018-11-26T02:00:25Z",
  "lastModifiedBy": "admin",
  "lastModifiedDate": "2018-11-26T02:00:25Z",
  "authorities": [
    "ROLE_USER",
    "ROLE_ADMIN"
  ]
}
```

* **异常情况：**400  login、email 已经存在

#### 6.用户更新信息

```
POST    http://localhost:8080/manager/account
```

* **接口说明：用户更新基本信息，login 不允许更改。**
* **参数说明：**

```
{
  "email": "bonismo@hotmail.com",
  "firstName": "string",
  "imageUrl": "string",
  "langKey": "en-US",
  "login":"bonismo",
  "lastName": "string"
}
```

* **返回结果：无**
* **异常情况：**
  * **400 邮箱已经存在**
  * **500 未登陆调用**

#### 7.修改登录密码（登录状态下）

```
POST    http://localhost:8080/manager/account/change-password
```

* **参数说明：**

```
{
  "currentPassword": "admin",
  "newPassword": "123456"
}
```

* **返回结果：无**
* **异常情况：400 密码不对**

#### 8.获取找回密码邮件（权限开放）

```
POST    http://localhost:8080/manager/account/reset-password/init
```

* **接口说明：输入邮箱，发送 RestKey，根据 RestKey 重置密码。**
* **参数说明：**

```
bonismo@hotmail.com
```

* **返回结果：**无
* **异常情况：400 邮箱并未注册**

#### 9.重置登录密码（权限开放）

```
POST    http://localhost:8080/manager/account/reset-password/finish
```

* **参数说明：**

```
{
  "key": "37238659946046171394",
  "newPassword": "123456"
}
```

* **返回结果：无**
* **异常情况：**
  * **400 密码长度不对**
  * **500 Key 不存在**

#### 10.获取当前用户信息

```
GET    http://localhost:8080/manager/account
```

* **返回结果：**

```
{
  "id": 3,
  "login": "admin",
  "firstName": "string",
  "lastName": "string",
  "email": "bonismo1@hotmail.com",
  "imageUrl": "string",
  "activated": true,
  "langKey": "string",
  "role": "ADMIN",
  "createdBy": "system",
  "createdDate": "2018-11-23T03:19:29Z",
  "lastModifiedBy": "admin",
  "lastModifiedDate": "2018-11-26T04:08:35Z",
  "authorities": [
    "ROLE_USER",
    "ROLE_ADMIN"
  ]
}
```

* **异常情况：500 未登陆调用**

#### 11.根据用户条件获取用户信息

```
GET    http://localhost:8080/manager/users/condition?[userId={userid}][login={login}]
```

* **接口使用说明：根据用户 id 或者 login 获取用户信息**
* **参数说明：**
  * **String login : **非必填参数
  * **Long userId : **非必填参数
* **返回结果：**
  * **当条件没有相应数据时，ResponseCode 404**

```
{
  "id": 3,
  "login": "admin",
  "firstName": "admin",
  "lastName": "",
  "email": "bonismo1@hotmail.com",
  "imageUrl": "string",
  "activated": true,
  "langKey": "zh-cn",
  "role": "ADMIN",
  "createdBy": "system",
  "createdDate": "2018-11-23T03:19:29Z",
  "lastModifiedBy": "admin",
  "lastModifiedDate": "2018-11-25T23:33:40Z",
  "authorities": [
    "ROLE_USER",
    "ROLE_ADMIN"
  ]
}
```

* **异常情况：无**

#### 12.获取所有用户信息

```
GET    http://localhost:8080/manager/users?[role={role}&][authority={authority}&]page={page}&size={size}&sort=[sort]
```

* **接口使用说明：**
  * **可根据 role、authority 进行查询**
  * **注意：使用 authority 查询时，sort 不能使用。（关系表没有主键）**
* **参数说明：**
  * **String role :  非必填参数 **
  * **String authority : 非必填参数**
  * **Integer page : 0**
  * **Integer Size : 5**
  * **Array Sort : id**
* **返回结果：**

```
[
  {
    "id": 1,
    "login": "system",
    "firstName": "System",
    "lastName": "",
    "email": "system@localhost.com",
    "imageUrl": "",
    "activated": true,
    "langKey": "zh-cn",
    "role": "ADMIN",
    "createdBy": "system",
    "createdDate": "2018-11-23T03:19:29Z",
    "lastModifiedBy": "admin",
    "lastModifiedDate": "2018-11-23T09:30:01Z",
    "authorities": [
      "ROLE_USER",
      "ROLE_ADMIN"
    ]
  },
  ......[other data]
]
```

* **异常情况：无**

#### 13.删除账户

```
DELETE    http://localhost:8080/manager/users/{login}
```

* **参数说明：**
  * **String login :**
* **返回结果：ResponseCode 200**
* **异常情况：无**



