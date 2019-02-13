### 一、绑定信息查询

#### 1.用户绑定信息（权限开放）

```
GET    http://localhost:8082/auth/user/bind/info/{login}
```

* **参数：**String **login  支持邮箱、手机号查询**
* **返回结果：**

```
{
  "googleSecret": "false",
  "mobileNum": "+86-17610016050",
  "emailNum": "32694110@qq.com",
  "currencyPassword": "false",
  "mobile": "true",
  "email": "true"
}
```

* **异常情况：**

  * **400  邮箱、手机格式不符合**
  * **410  多账号绑定同一手机号，不支持查询**
  * **404  用户不存在**

---

### 二、谷歌两步验证码

#### 1.获取随机谷歌秘钥（权限开放）

```
GET    http://localhost:8082/auth/user/bind/g-auth/random
```

* **返回结果：**

```
HMMFF3HEEQRMO74S
```

* **异常情况：无**

#### 2.绑定前验证秘钥和验证码是否正确

```
POST    http://localhost:8082/auth/user/bind/g-auth/check
```

* **参数说明：**

```
{
  "secret":"GU6SHXZJYYCJXYYQ",
  "gaCode":"894647"
}
```

* **返回结果：**

```
true / false
```

* **异常情况：400  参数为空**

#### 3. 绑定、更新谷歌秘钥

```
GET    http://localhost:8082/auth/user/bind/g-auth/create/{secret}
```

* **参数说明：**String **secret  ** **\[ 自动根据当前登录用户，获取用户的 userId  \]**
* **返回结果：**

```
{
  "id": 1,
  "userId": 3,
  "googleSecret": "GU6SHXZJYYCJXYYQ",
  "currencyPassword": null,
  "createdBy": "1010",
  "createdDate": "2018-06-20T13:24:02Z",
  "lastModifiedBy": "1010",
  "lastModifiedDate": "2018-06-20T13:24:02Z"
}
```

* **异常情况：500 当前用户没有登录，调用该接口（正常逻辑不会出现）**

#### 4. 展示谷歌两步验证二维码 （目前该接口测试使用，生产环境前端拼接展示）

```
GET    http://localhost:8082/auth/user/bind/g-auth/display?width=300&height=300
```

* 参数1：int **width  \[ 默认值300 \]**
* 参数2：int **heigth  \[ 默认值300 \]**
* **该 URL 放入&lt;img src="" /&gt; 显示**

#### 5. 验证谷歌两步验证码（权限开放）

```
GET    http://localhost:8082/auth/user/bind/g-auth/verify/{login}/{gaCode}
```

* **参数：**

* * String **login  可以是邮箱或手机号**
  * String **gaCode**
* **返回结果：**

  * **true \[ 验证成功 \] **
  * **false \[ 验证失败 / 用户并没有绑定秘钥 \]**

* **异常情况：**

  * **400 邮件格式、手机格式不正确**
  * **410  多账号绑定同一手机号，不支持查询**
  * **404 当前用户不存在**

  * **404 当前用户没有绑定 GA **



