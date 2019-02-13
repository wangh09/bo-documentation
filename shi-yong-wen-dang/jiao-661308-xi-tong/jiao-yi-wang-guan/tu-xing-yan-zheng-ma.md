## 图形验证码

#### 获取图形验证码

```
GET    http://47.92.88.235:8082/security/captcha/display
```

* 返回结果
  * ![](/assets/1529505540078.jpg)

#### 校验图形验证码

```
POST    http://47.92.88.235:8082/security/captcha/verify
```

* 参数：
  * ```
    {
        "captchaCode":"38bv"
    }
    ```
* 返回结果：

  * true **\[ 验证成功 \]**

  * false **\[ 验证失败 \]**



