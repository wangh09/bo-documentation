## KYC 功能 /kyc

本模块主要用户的一些其他信息：身份证、驾驶证、护照其中一种信息

---

| KYC 级别 | 自动、人工可配置化 | 支持证件类型 | 第三方服务 |
| :--- | :--- | :--- | :--- |
| **C1** | **支持** | **身份证、驾驶证、护照** |  |
| **C2** | **支持** | **身份证、驾驶证、护照** | **ALiYun数据采集、OSS / S3** |
| **C3** | **支持** | **暂无** | **暂无** |

---

| **KYC 状态** | PASSED | PENDING | REJECTED |
| :--- | :--- | :--- | :--- |


---

#### KYC 配置说明（根据 cerotificateLevel、countryCode 匹配，0代表当前级别如果匹配不上使用该认证）

```
    kyc:
        # 如果 level 是 aLiYunOcr2，采用第三方服务。
        # 如果 level 是 c1，匹配 autoPass,manual,autoDeny 三个 countryCode,匹配成功，使用该类型。
        # 匹配失败，取 c1 的 value，判断有没有0，如果是0，使用该服务，如果匹配不上，使用 defaultType。
        defaultType: autoDeny
        autoPass:
            - c1: 0
            - c2: 0
        manual:
            - c1: 86
            - c2: 90,21
            - normal: 0
        autoDeny:
            - c3: 91,22
        thirdService:
            aLiYunOcr:
                ocrCountryCode:
                    - aLiYunOcr2:
                aLiYunAppCode: 801dadf2bb0c47829d8dcc58fd863abb
                ocrIdentityHost: http://dm-51.data.aliyun.com
                ocrIdentityPath: /rest/160601/ocr/ocr_idcard.json
                ocrVehicleHost: https://dm-52.data.aliyun.com
                ocrVehiclePath: /rest/160601/ocr/ocr_driver_license.json
                ocrPassportHost: https://ocrhz.market.alicloudapi.com
                ocrPassportPath: /rest/160601/ocr/ocr_passport.json
```

---

#### 1.KYC 认证

```
POST    http://localhost:8082/auth/kyc/certificate
```

* **具体流程：**

  * 用户认证级别属于审核状态内配置，Default Verification 从配置中匹配当前认证级别和国家代码属于哪种认证状态，设置该认证状态，然后封装使用 Object-Storage Service 返回的key 和 address数据，使用 RestTemplate发送 Http 请求到UAA微服务，获取当前请求的用户 id，保存到数据库。
  * 用户认证级别属于第三方服务的级别，匹配用户提交的国家代码，进入China Verification，解析使用Object-Storage Service返回的 address，调用阿里云OCR服务扫描用户图片地址，用户KYC认证状态设置为人工审核。使用 RestTemplate发送 Http 请求到UAA微服务，获取当前请求的用户 id，保存到数据库。

* **流程图：**

![](/assets/KYC 认证.png)

* **参数说明：**

  * String **certificateLevel 认证级别（normal、C1、C2、C3、aLiYunOcr2 等，具体级别由配置文件决定** **）**
  * String **countryCode  国家电话代码  **

  * String **data 表单数据**

* **参数：**

```
{
  "certificateLevel": "string",
  "countryCode": "string",
  "data": "string",
}
```

* **返回结果：**

```
PASSED / PENDING / REJECTED
```

* **异常情况：**

  * **400 认证级别不符合要求（如C1认证后，跳过C2进行C3认证）**
  * **500 当前用户没有登录，调用该接口（正常逻辑不会出现）**

#### 2.证件照片上传

```
POST    http://localhost:8082/auth/kyc/upload
```

* **参数：**MultiPartFile
* **返回结果：**

```
{
  "ossKey": "e71a734278414741a164c4fa00884f97.jpg",
  "ossUrl": "//ink-assets.oss-cn-beijing.aliyuncs.com/license-ocr/e71a734278414741a164c4fa00884f97.jpg"
}
```

* **异常情况：**
  * **500 上传失败**

#### 3.查询 KYC 认证状态

```
GET    http://localhost:8082/auth/kyc/status
```

* **接口说明：当认证时，先调用该接口，查看用户是否认证。如果 C1认证通过，根据 C1认证类型、认证国家，让用户在 C2认证时，依照认证类型、认证国家继续认证 C2。**

  * **注：C1 和 C2认证类型必须一致。C2 认证时，需要显示国家、真实姓名、证件号码，具体数据存储在 kycData 。**

* **返回参数：**

```
用户未认证返回的数据
{
  "passExpire" : null,
  "kycStatus" : null,
  "currencyPassExpire" : null,
  "mapiPass" : null,
  "passLimit" : false,
  "currencyPassLimit" : false,
  "mobileLimit" : false,
  "gaLimit" : false,
  "gaExpire" : null,
  "mobileExpire" : null
}
```

```
用户认证后的数据 
{
  "kycWithdrawManual":"50"
  "passExpire": null,
  "kycStatus": "C3_PASSED",
  "kycWithdrawManual": "50",
  "passLimit": false,
  "gaLimit": false,
  "currencyPassExpire": null,
  "mapiPass": "C3",
  "kycData": "{\"fullName\":{\"type\":\"text\",\"data\":\"龚涛\"},\"birthday\":{\"type\":\"select\",\"data\":\"2017-2-2\"},\"country\":{\"type\":\"text\",\"data\":\"China (中国)\"},\"city\":{\"type\":\"text\",\"data\":\"海淀区\"},\"address\":{\"type\":\"text\",\"data\":\"123\"},\"postalCode\":{\"type\":\"text\",\"data\":\"10010\"},\"documentType\":{\"type\":\"select\",\"data\":\"1\"},\"residenceProofType\":{\"type\":\"select\",\"data\":\"bankStatement\"},\"front\":{\"key\":\"aa66252f39c347bba64e52a51639dfd7.png\",\"url\":\"//ink-assets.oss-cn-beijing.aliyuncs.com/license-ocr/aa66252f39c347bba64e52a51639dfd7.png\",\"type\":\"image\"},\"back\":{\"key\":\"d9b259c09f204fa49716c9ac0cb2b002.png\",\"url\":\"//ink-assets.oss-cn-beijing.aliyuncs.com/license-ocr/d9b259c09f204fa49716c9ac0cb2b002.png\",\"type\":\"image\"},\"handheld\":{\"key\":\"02e111bbe38044b49a1a23880f8c6558.png\",\"url\":\"//ink-assets.oss-cn-beijing.aliyuncs.com/license-ocr/02e111bbe38044b49a1a23880f8c6558.png\",\"type\":\"image\"},\"bankStatement\":{\"key\":\"243d4681d65c4bf0b999f0deb27fcc8e.jpg\",\"url\":\"//ink-assets.oss-cn-beijing.aliyuncs.com/license-ocr/243d4681d65c4bf0b999f0deb27fcc8e.jpg\",\"type\":\"image\"}}",
  "currencyPassLimit": false,
  "kycLimit": "100",
  "mobileLimit": false,
  "gaExpire": null,
  "mobileExpire": null,
  "kycCountryCode": "86"
}
```

* **异常情况：500 当前用户没有登录，调用该接口（正常逻辑不会出现）**

* **重要返回参数说明：**

  * String** kycWithdrawManual : 比如 C3 提现额度为100，假设配置 kycWithdrawManual 的值为50，则 mapi 会根据该值从自动提现转为人工审核提现。 该字段只有在某一级别配置时，且认证状态为PASSED**

  * String **mapiPass : mapi 模块判断用户提现级别**

  * String **kycLimit 显示用户提现额度，用来计算展示用户剩余提现额度**

  * **用户修改密码，24小时内不能提现限制： Boolean 类型，true 标识用户已限制提现，Expire 结尾字段有值，false 未限制，Expire 结尾字段为 null**

    * Boolean **passLimit **

    * Long **passExpire**

    * Boolean **currencyPassLimit**

    * Long **currencyPassExpirre**

    * Boolean **mobileLimit**

    * Long **mobileExpire**

    * Boolean **gaLimit**

    * Long **gaExipre**

#### 4.获取 KYC 认证级别的提现额度

```
GET    http://localhost:8082/auth/kyc/withdraw/limit
```

* 返回参数：

```
[
  {
    "id": 1,
    "kycLevel": "C0",
    "withdrawLimit": 0
  },
  {
    "id": 2,
    "kycLevel": "C1",
    "withdrawLimit": 2
  },
  {
    "id": 3,
    "kycLevel": "C2",
    "withdrawLimit": 10
  },
  {
    "id": 4,
    "kycLevel": "C3",
    "withdrawLimit": 100
  }
]
```

* **异常情况：无**

---

#### 5.提升用户提现额度 \[ 该功能暂时不使用 \]

```
POST    http://localhost:8082/auth/kyc/upgrade/vip-withdraw
```

* **接口场景说明：**

  * 根据底层账户，或者别的用户等级，手动给用户提升提现级别（额度），或者用户申请。

* **参数说明：**

  * 必填参数：userId、vipLevel、withdrawLimit
  * 更新补填：status  （管理后台操作）

```
{
  "status": true,
  "userId": 12,
  "vipLevel": "1",
  "withdrawLimit": 100
}
```

* **返回结果：**

```
{
  "id": 2,
  "userId": 12,
  "vipLevel": "1",
  "withdrawLimit": 100,
  "status": true
}
```



