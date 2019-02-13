## 谷歌两步验证码 \[ 请求都已改成 GET，已部署 \]

#### 绑定谷歌秘钥

```
GET    http://47.92.88.235:8082/auth/g-auth/create
```

* 不传参数 **\[ 自动根据当前登录用户，获取用户的 userId  \]**
* 返回结果
  * ```
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

#### 展示谷歌秘钥

```
GET    http://47.92.88.235:8082/auth/g-auth/info
```

* 返回结果
  * ```
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

#### 展示谷歌两步验证二维码

```
GET    http://47.92.88.235:8082/auth/g-auth/display?width=300&height=300
```

* 参数1：int **width  \[ 默认值300 \]**
* 参数2：int **heigth  \[ 默认值300 \]**
* **该 URL 放入&lt;img src="" /&gt; 使用就显示了**

#### 重置谷歌两步验证二维码

```
GET    http://47.92.88.235:8082/auth/g-auth/reset
```

* 返回结果
  * ```
    {
      "id": 1,
      "userId": 3,
      "googleSecret": "TY4RHNNERPYBTK62",
      "currencyPassword": null
    }
    ```

#### 验证谷歌两步验证码

```
GET    http://47.92.88.235:8082/auth/g-auth/verify/{gaCode}
```

* 参数：String **gaCode**
* 返回结果：
  * **true \[ 验证成功 \] **
  * **false \[ 验证失败 \]**

#### 移除谷歌两步验证码

```
GET    http://47.92.88.235:8082/auth/g-auth/remove
```

* **移除谷歌两步验证码会自动清空用户资金安全密码（慎用）**
* **移除谷歌验证码后，不能调用绑定谷歌秘钥的接口（/auth/g-auth/create），会报 400 错误，Secret Code user id already exists。应该调用重置接口（/auth/g-auth/reset）。可以根据实际需求，推荐用户重新设置资金安全密码。**
* 无返回结果



