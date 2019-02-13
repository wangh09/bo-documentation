## 账户相关功能  /account

#### 1.获取账户信息

```
GET    http://47.92.88.235:8082/mapi/account/get
```

* 参数：
  * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常
* 返回结果：

  * ```
    {
      "title": "get mat-user info",
      "status": 200,
      "data": {
        "id": 100003,
        "canSignin": true,
        "canTrade": true,
        "canWithdraw": true,
        "createdAt": 1527044943863,
        "level": 0,
        "type": "TRADER",
        "updatedAt": 1527044943863
      },
      "timestamp": 1529587370679
    }
    ```

#### 2.创建账户信息

```
POST    http://47.92.88.235:8082/mapi/account/create
```

* 参数：

  ```
  {
    "canTrade": true,     //能否交易
    "canWithdraw": true    //能否提现
  }
  ```

* 返回结果：

  * ```
    {
      "title": "create mat-user info",
      "status": 200,
      "data": {
        "id": 100014,
        "canSignin": true,
        "canTrade": true,
        "canWithdraw": true,
        "createdAt": 1529587686246,
        "level": 0,
        "type": "TRADER",
        "updatedAt": 1529587686246
      },
      "timestamp": 1529587686261
    }
    ```

#### 3.更新账户信息

```
POST    http://47.92.88.235:8082/mapi/account/update
```

* 参数：获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常

  ```
  {
    "canTrade": true,     //能否交易
    "canWithdraw": true    //能否提现
  }
  ```

* 返回结果：

  * ```
    {
      "title": "create mat-user info",
      "status": 200,
      "data": {
        "id": 100014,
        "canSignin": true,
        "canTrade": true,
        "canWithdraw": true,
        "createdAt": 1529587686246,
        "level": 0,
        "type": "TRADER",
        "updatedAt": 1529587686246
      },
      "timestamp": 1529587686261
    }
    ```



