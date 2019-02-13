## 检查用户注册的邮箱是否存在

```
GET    http://47.92.88.235:8082/security/email/check/{email}
```

* 参数：String **email**
* 返回结果：
  * **true  **\[ 邮箱已存在，提示用户更换邮箱注册 \]
  * **false **\[ 邮箱不存在，用户可以注册 \]

## 邮箱验证码

#### 发送邮箱注册验证码 \[ 有效时间为7分钟，提示最好为5分钟，因为用户注册信息要写入数据库 \]

```
GET    http://47.92.88.235:8082/security/email/send/{email}/{type}/{language}
```

* 参数1：String **email**

* 参数2：String **type**

  * **reg : 注册**
    * 邮件模板
      > 亲爱的[32694110@qq.com](mailto:32694110@qq.com)
      >
      > 您的 uaa 账号已创建成功, 请输入下边的激活码到网站的对应窗口:
      >
      > 53119718146978247234
      >
      > Regards,  
      > _inkUaa 团队._

* 参数3：String **language \[**目前测试，线上只有英文，待检查，本地测试为多语言**\]**
  * * **en : 英文**
    * **cn : 中文**
    * **ko : 韩文**
    * **ja  : 日文**
* **无返回值**

#### 验证邮箱注册码

```
GET    http://47.92.88.235:8082/auth/email/verify/{email}/{code}
```

* 参数1：String **email**
* 参数2：String **code**

* 返回结果：

  * true **\[ 验证码正确 \]**

  * false **\[ 验证码错误或失效 \]**



