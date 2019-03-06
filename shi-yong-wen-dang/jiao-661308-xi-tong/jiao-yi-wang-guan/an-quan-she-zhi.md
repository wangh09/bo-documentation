## 公共信息认证  /security

本模块包含基本的安全认证功能，包括：短信验证码、邮箱验证码、谷歌验证码、图形验证码。

---

### 一、短信验证码

#### 短信配置及相关说明

```
    sms:
        defaultProvider: twilio                           # 默认短信服务商
        appName: 【INKubator】                             # 通用短信模板配置的应用名称
        aLiYun:                                           # ALiYun 短信服务商
            countryCode: 86                               # 当匹配到用户国家电话代码使用该服务商
            product: Dysmsapi
            domain: dysmsapi.aliyuncs.com
            accessKeyId: 
            accessKeySecret: 
            signName: 阿里云短信测试专用
            templates:                                    # 阿里云定制模板编号
                # CN
                regTemCN: SMS_134200343
                ......
        nexmo:                                            # Nexmo 短信服务商
            countryCode:                                  # 当匹配到用户国家电话代码使用该服务商
            apiKey: 
            apiSecret: 
            fromNumber: 
        twilio:                                           # Twilio 短信服务商 
            countryCode:                                  # 当匹配到用户国家电话代码使用该服务商
            accountId: 
            authToken: 
            fromNumber: 
        commonTemplates:                                  # 通用短信模板配置
            # CN
            regTemCN: ${application.sms.appName} 您当前注册的 INKubator 交易所，验证码：%s 。5分钟内有效，请勿告诉他人。
            loginTemCN: ${application.sms.appName} 您当前正在登录 INKubator 交易所，验证码：%s 。5分钟内有效，请勿告诉他人。                
            ......
```

#### 短信发送流程

```
                                                |----> ALiYun ----->|
          86 / 65                match success  |                   |      
Send SMS ---------> countryCode --------------->|----> Twilio ----->|=====> Send Success
                         |                      |                   |
            match failed |                      |----> Nexmo  ----->|
                         |                                          |
                         |--------------------> defaultProvider --->|
```

#### 1. 发送短信验证码（权限开放）

```
GET    http://localhost:8082/security/sms/send/{mobile}/{type}/{content}
```

* **接口说明：短信验证码有效时间 5 分钟，可以开启或关闭一次性验证。**

* **参数1：**String **mobile**

  * 电话号码可以传入类似 **+86-138\*\*\*\*\*\*\*\***

* **参数2：**String **type 短信类型**

  * **regCN  用户注册的中文模板**

  * **loginCN  用户登录验证的中文模板**

  * **loginNoticeCN 用户登录通知的中文模板，该模板后台自动发送**

  * **changePassCN  重置登录密码的中文模板**

  * **resetPassCN  修改登录密码的中文模板**

  * **bindMobileCN  绑定手机号码的中文模板**

  * **changOldMobileCN  修改手机号码的旧手机中文模板**

  * **changeNewMobileCN  修改手机号码的新手机中文模板**

  * **bindGACN  绑定 GA 的中文模板**

  * **resetGACN  重置 GA 的中文模板**

  * **setCurrencyCN  设置资金安全密码的中文模板**

  * **resetCurrencyCN  重置资金安全密码的中文模板  **

  * **currencyRateCN  设置24小时免密码的资金安全密码的中文模板**

  * **addWithdrawAddressCN  添加提现地址的中文模板**

  * **withdrawCN  提现的中文模板（content）**

  * **withdrawConfirmCN  提现到账的中文模板（content）**

  * **withdrawNoticeCN  用户提现通知中文模板（content）**

  * **setApiKeyCN  用户新建 API 中文模板**

  * **checkApiKeyCN  用户查看 API 中文模板**

  * * **EN、KR、JP 后缀同上**
  * **参数3 ：**String **content **
    * ** 文本内容（具体使用需要对照模板的占位符）**

* **返回结果：**

```
{
  "dayLimit": 10,
  "hourLimit": 5,
  "minuteLimit": 3,
  "smsResult": "smsSuccess"
  ["expire":3000]
}
```

* **返回结果重要参数说明：**

  * Long **dayLimit  24小时内同一模板短信发送限制**

  * Long **hourLimit  小时内同一模板发送限制**

  * Long **minuteLimit  分钟内同一模板发送限制**

  * String **smsResult  返回结果**

    * **smsSuccess  发送成功**

    * **smsFailed  欠费、网络情况等**

    * **smsTry  重新发送（国外服务商网络问题）**

    * **smsMinuteLimit  分钟级别限制**

    * **smsHourLimit  小时级别限制**

    * **smsDayLimit  天级别限制**

    * **expire  如果是 Limit 限制级别，则该字段存在，有值且单位为秒**

* **异常情况： 400  手机号码不符合规则、短信模板不存在**

#### 2. 验证短信验证码（权限开放）

```
GET    http://localhost:8082/security/sms/verify/{type}/{mobile}/{code}
```

* **参数1：**String **type  短信模板**

* **参数2：**String **mobile  手机号码 （+86-138\*\*\*\*\*）**

* **参数3：**String **code  6 位验证码**

* **返回结果：**

  * **验证成功**
    * **checkSuccess**
  * **验证失败**
    * **checkFailed**
  * **验证超时**
    * **checkNotExists**

* **异常情况： 400 手机号码不符合规则**

---

### 二、邮箱验证码

#### 1.验证邮箱是否可以注册（权限开放）

```
http://localhost:8082/auth/user/email/check/{email}
```

* **参数说明：**
  * String **email  **
* **返回结果：true 证明邮箱存在，不能注册，false 反之。**

```
true / false
```

* **异常情况：无**

#### 2. 发送邮箱注册验证码（权限开放）

```
GET    http://localhost:8082/security/email/send/{email}/{type}/{language}
```

* **接口说明：由于邮件异步发送，且没有返回值，所以默认发送成功，邮件服务商造成的退信等情况并不会返回到发送结果。**

* **参数1：**String **email 格式参考相关逻辑**

* **参数2：**String **type**

  * **activationKeyEmail，activationLinkEmail  用户注册时，激活码（参考注册&登录的激活类型）**
    * 邮件模板
      > 亲爱的[32694110@qq.com](mailto:32694110@qq.com)
      >
      > 您的 uaa 账号已创建成功, 请输入下边的激活码到网站的对应窗口:
      >
      > 53119718146978247234
      >
      > Regards,  
      > _inkUaa 团队._
  * **welcomeEmail  用户注册欢迎邮件，后台直接调用。**

  * **bindMobileEmail  用户绑定手机号验证码邮件**

  * **changeMobileEmail  用户更改手机号验证码邮件**

  * **resetPasswordEmail  用户重置密码验证码邮件**

  * **resetCurrencyPassEmail  用户重置资金验证码邮件**

  * **bindGAEmail 用户绑定 GA 验证码邮件**

  * **resetGAEmail 用户重置 GA 验证码邮件**

* **参数3：**String **language**

  * * **en-US : 英文**
    * **zh-CN : 中文**
    * **ko-KR : 韩文**
    * **ja-JP  : 日文**

* **返回结果：**

```
{
  "dayLimit": 10,
  "hourLimit": 5,
  "minuteLimit": 3,
  "emailResult": "emailSuccess"
  ["expire":300]
}
```

* **返回结果说明：**

  * Long **dayLimit  24小时内发送同一模板限制 **

  * Long **hourLimit  小时内发送同一模板限制**

  * Long **minuteLimit  分钟内发送同一模板限制**

  * **发送结果：**

    * String **emailSuccess  发送成功**

    * String **emailMinuteLimit  分钟级别限制**

    * String **emailHourLimit  小时级别限制**

    * String **emailDayLimit  天级别限制**

  * Long** expire 仅当 emailResult 的值以 Limiit 结尾时，该字段存在，有值且单位为秒**

#### 3. 验证邮箱注册码（权限开放）

```
GET    http://localhost:8082/security/email/verify/{type}/{email}/{key}
```

* **参数1：**String **type  邮件模板**
* **参数2：**String** email  支持格式参考相关逻辑**
* **参数3：**String **code  验证码**

* **返回结果：**

  * true **\[ 验证码正确 \]**

  * false **\[ 验证码错误或失效 \]**

* **异常情况：无**

---

## 三、图形验证码

**config 模块，gateway-dev/prod.yml 配置图像验证码开关**

```
    captcha:
        geetestSwitch: true
        geetestId: 44d6e413fd041e7a8e61bd6d72d54b1d
        geetestKey: de504e76598c8b022f58aa93127a21e5
        newFailBack: true
```

* **geetestSwitch：true 默认调用 极验验证。 false 调用图形验证。**

#### **1.获取图形验证码开关**（权限开放）

```
GET    http://localhost:8082/security/captcha
```

* **返回结果：**
  * true  使用** 极验验证**
  * false 使用 **图形验证**
* **异常情况：无**

#### 2. 获取图形验证码（权限开放）

```
GET    http://localhost:8082/security/captcha/display
```

* **返回结果：**
* \(图形验证码返回结果\)

![](/assets/1529505540078.jpg)

* \(极验验证返回结果\)
  * **参数说明：**“success" 值为1，证明极验初始化成功。

```
{"success":1,"challenge":"f536103d721b8105bf758b65940dbf37","gt":"44d6e413fd041e7a8e61bd6d72d54b1d"}
```

* **异常情况：无**

#### 3. 校验图形验证码（权限开放）

```
POST   http://localhost:8082/security/captcha/verify
```

* **参数说明：**

  * captchaCode: 图形验证码传输参数，其余三个为极验验证码传输参数

```
{
  "captchaCode": "string",
  "geetestChallenge": "string",
  "geetestSeccode": "string",
  "geetestValidate": "string"
}
```

* **返回结果：**

  * true **\[ 验证成功 \]**

  * false **\[ 验证失败 \]**

* **异常情况：无**



