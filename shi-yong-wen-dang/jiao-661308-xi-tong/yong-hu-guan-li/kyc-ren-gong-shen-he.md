#### 1.KYC 审核

```
POST    http://localhost:8080/user/kyc/level/approve
```

* **参数：**

```
{
  "userId": 5,
  "countryCode": "86",
  "certificateLevel": "normal",
  "certificateStatus": "PASSED",
  "data": "{\"fullName\":{\"type\":\"text\",\"data\":\"龚涛\"},\"birthday\":{\"type\":\"select\",\"data\":\"2017-2-2\"},\"country\":{\"type\":\"text\",\"data\":\"China (中国)\"},\"city\":{\"type\":\"text\",\"data\":\"海淀区\"},\"address\":{\"type\":\"text\",\"data\":\"123\"},\"postalCode\":{\"type\":\"text\",\"data\":\"10010\"},\"documentType\":{\"type\":\"select\",\"data\":\"1\"},\"residenceProofType\":{\"type\":\"select\",\"data\":\"bankStatement\"},\"front\":{\"key\":\"aa66252f39c347bba64e52a51639dfd7.png\",\"url\":\"//ink-assets.oss-cn-beijing.aliyuncs.com/license-ocr/aa66252f39c347bba64e52a51639dfd7.png\",\"type\":\"image\"},\"back\":{\"key\":\"d9b259c09f204fa49716c9ac0cb2b002.png\",\"url\":\"//ink-assets.oss-cn-beijing.aliyuncs.com/license-ocr/d9b259c09f204fa49716c9ac0cb2b002.png\",\"type\":\"image\"},\"handheld\":{\"key\":\"02e111bbe38044b49a1a23880f8c6558.png\",\"url\":\"//ink-assets.oss-cn-beijing.aliyuncs.com/license-ocr/02e111bbe38044b49a1a23880f8c6558.png\",\"type\":\"image\"},\"bankStatement\":{\"key\":\"243d4681d65c4bf0b999f0deb27fcc8e.jpg\",\"url\":\"//ink-assets.oss-cn-beijing.aliyuncs.com/license-ocr/243d4681d65c4bf0b999f0deb27fcc8e.jpg\",\"type\":\"image\"}}",
  "extraData": null,
  "description": null,
  "extension": null
}
```

* **返回结果：**

```
{
  "id": 6,
  "userId": 5,
  "countryCode": "86",
  "certificateLevel": "normal",
  "certificateStatus": "PASSED",
  "data": "{\"fullName\":{\"type\":\"text\",\"data\":\"龚涛\"},\"birthday\":{\"type\":\"select\",\"data\":\"2017-2-2\"},\"country\":{\"type\":\"text\",\"data\":\"China (中国)\"},\"city\":{\"type\":\"text\",\"data\":\"海淀区\"},\"address\":{\"type\":\"text\",\"data\":\"123\"},\"postalCode\":{\"type\":\"text\",\"data\":\"10010\"},\"documentType\":{\"type\":\"select\",\"data\":\"1\"},\"residenceProofType\":{\"type\":\"select\",\"data\":\"bankStatement\"},\"front\":{\"key\":\"aa66252f39c347bba64e52a51639dfd7.png\",\"url\":\"//ink-assets.oss-cn-beijing.aliyuncs.com/license-ocr/aa66252f39c347bba64e52a51639dfd7.png\",\"type\":\"image\"},\"back\":{\"key\":\"d9b259c09f204fa49716c9ac0cb2b002.png\",\"url\":\"//ink-assets.oss-cn-beijing.aliyuncs.com/license-ocr/d9b259c09f204fa49716c9ac0cb2b002.png\",\"type\":\"image\"},\"handheld\":{\"key\":\"02e111bbe38044b49a1a23880f8c6558.png\",\"url\":\"//ink-assets.oss-cn-beijing.aliyuncs.com/license-ocr/02e111bbe38044b49a1a23880f8c6558.png\",\"type\":\"image\"},\"bankStatement\":{\"key\":\"243d4681d65c4bf0b999f0deb27fcc8e.jpg\",\"url\":\"//ink-assets.oss-cn-beijing.aliyuncs.com/license-ocr/243d4681d65c4bf0b999f0deb27fcc8e.jpg\",\"type\":\"image\"}}",
  "extraData": null,
  "description": null,
  "extension": null,
  "createdBy": "10089",
  "createdDate": "2018-11-09T03:48:31Z",
  "lastModifiedBy": "anonymousUser",
  "lastModifiedDate": "2018-11-09T18:49:11Z"
}
```

* **异常情况：500 用户不存在**

#### 2.删除照片数据

```
DELETE    http://localhost:8080/user/kyc/rejected/licence-img/{fileKey}
```

* **接口说明：**
  * 人工审核在拒绝时，调用该接口，删除用户上传照片数据。
* **参数说明：**
  * String** fileKey :  图片Key**
* **返回结果：无**
* **异常情况：无**



