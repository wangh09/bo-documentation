## 短信验证码

#### 发送短信验证码 \[ 有效期为 5 分钟 \]

```
GET    http://47.92.88.235:8082/security/sms/send/{mobile}
```

* 参数：String **mobile**

  * 电话号码可以传入类似 **+861-138\*\*\*\*\*\*\*\***，也可以传入**138\*\*\*\*\*\*\*\*。目前使用阿里短信接口，暂时不支持+86 等，后期更换为 NEXMO 支持。**

* 返回结果

  * 发送成功

    * send\_sms\_success

  * 发送失败** \[ 一般情况为欠费、网络问题 \]**

    * send\_sms\_failed

#### 验证短信验证码

```
GET    http://47.92.88.235:8082/security/sms/verify/{mobile}/{code}
```

* 参数1：String **mobile**

* 参数2：String **code**

* 返回结果：

  * 验证成功
    * check\_success
  *  验证失败

    * check\_failed

  * 验证码不存在** \[ 验证码超时 \]**

    * check\_notExists



