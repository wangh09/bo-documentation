### 三、通用资金密码

#### 1. 设置资金安全密码（长度 6 - 16）

```
POST    http://localhost:8082/auth/user/bind/currency-pass
```

* **参数：**

```
{ "pass":"123456" }
```

* **返回结果：**

```
true / false
```

* **异常情况：**

  * **400 资金密码长度不够、资金密码和登录密码一样**
  * **500 当前用户没有登录，调用该接口（正常逻辑不会出现）**

#### 2. 根据旧密码设置新的安全资金密码

```
PUT   http://localhost:8082/auth/user/bind/currency-pass/change
```

* **参数：**

```
{
  "oldPass":"123456",
  "newPass":"abcde"
}
```

* **返回结果：**

```
true / false
```

* **异常情况：**

  * **400  密码为空**

  * **400 用户登录密码和资金密码相同 **

  * **500 当前用户没有登录，调用该接口（正常逻辑不会出现）**

#### 3. 验证资金安全密码是否正确

```
POST    http://localhost:8082/auth/user/bind/currency-pass/verify
```

* **参数：**

```
{"pass":"123456"}
```

* **返回结果：**

```
true / false
```

* **异常情况：**
  * **404  用户找不到**
  * **500 当前用户没有登录，调用该接口（正常逻辑不会出现）**

#### 4.按时间段输入资金安全密码

```
GET   http://localhost:8082/auth/user/bind/currency-pass/settings/{rate}
```

* **参数：**String **rate**  **1/2/3**

  * 1 为每次输入资金安全密码
  * 2 为每小时输入资金安全密码，该资金状态默认
  * 3 为 24 内免输入资金安全密码

* **返回结果：**

  * successEvery **\[ 每次 \]**

  * successHour **\[ 1小时 \]**

  * successDay **\[ 24小时 \]**

* **异常情况：**

  * **400  rate 不对**

  * **500 当前用户没有登录，调用该接口（正常逻辑不会出现）**

#### 5.获取用户的资金安全密码设置状态

```
GET    http://localhost:8082/auth/user/bind/currency-pass/settings/status
```

* **返回结果：**

  * String **currencyRateStatus  资金安全密码频率**
    * 1  **\[ 每次 \] （没有过期时间，永久存在 ）**
    * 2  **\[ 1小时 \] （状态为1小时，当状态消失，自动设置为1）**
    * 3  **\[ 24小时 \] （状态为24小时，当状态消失，自动设置为1）**
  * String **rateExpire  当前状态剩余的时间（单位：秒）**

```
{
  "rateExpire": 3002,
  "currencyRateStatus": "2"
}
```

* **异常情况：500 当前用户没有登录，调用该接口（正常逻辑不会出现）**

#### 6.校验用户资金密码（当 currency\_tate\_status = 2 / 3 时，调用该接口）

```
GET    http://localhost:8082/auth/user/bind/currency-pass/verify-by-status
```

* **（当 currencyRateStatus = 2 / 3 时，调用该接口，建议 rateExpire 小于 60-90内，强制用户输入资金安全密码）**

* **返回结果：**

  * true **自动验证通过**
  * false **验证失败，或者用户 currencyRateStatus = 1调用了该接口，让用户手动输入资金安全密码**

```
true / false
```

* **异常情况：**

  * **500 当前用户没有登录，调用该接口（正常逻辑不会出现）**



