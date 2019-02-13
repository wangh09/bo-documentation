#### 1.KYC  C1 审核

```
GET    http://localhost:8080/user/approve/kyc-one-status/1/PENDING
```

* **接口说明：**
  * 当用户的国家是 **China \(中国\) **时，会自动调用阿里云的 **身份证 / 驾驶证 **进行自动审核。**护照 **因为国内没有相关服务，所以会自动审核通过。
  * 当用户的国家不是 **China \(中国\) **时，C1 认证全部审核通过。
  * **所以该接口一般不需要调用，正常状态都是 PASSED**
* 参数说明：
  * Long **userId**
  * String **PENDING / PASSED / REJECTED**
* 返回结果：
  * ```
    {
      "id": 1,
      "userId": 1,
      "familyName": "Admin",
      "givenName": "admin",
      "countryName": "",
      "sex": null,
      "idNum": null,
      "realName": null,
      "birthday": null,
      "province": null,
      "city": null,
      "prefecture": null,
      "idSuccess": null,
      "vehicleName": null,
      "vehicleType": null,
      "vehicleStart": null,
      "vehicleEnd": null,
      "vehicleNum": null,
      "archiveNo": null,
      "vehicleSuccess": null,
      "passportNum": null,
      "passSuccess": null,
      "licenceType": "IDENTITY",
      "verifyStatus": "PENDING",
      "createdBy": "",
      "createdDate": "2018-09-09T12:23:17Z",
      "lastModifiedBy": "10089",
      "lastModifiedDate": "2018-09-10T15:29:26Z"
    }
    ```

#### 2.KYC C2 审核

```
GET    http://localhost:8080/user/approve/kyc-two-status/1/PENDING
```

* **接口说明：**
  * 当用户的国家是 **China \(中国\) **时，会自动调用阿里云的 **身份证 / 驾驶证 / 护照 **先进行 **OCR **扫描相关信息，然后上传到阿里云的 **OSS **服务器。
  * 当用户的国家不是 **China \(中国\) **时，只使用阿里云的 **OSS** 服务器。
* 参数说明：
  * Long  userId
  * String **PENDING / PASSED / REJECTED**
* 返回结果：
  * ```
    {
      "id": 1,
      "userId": 1,
      "sex": "男",
      "birthday": null,
      "idAddress": null,
      "idName": null,
      "nationality": null,
      "idCardNum": null,
      "idFaceSuccess": null,
      "startDate": null,
      "endDate": null,
      "issue": null,
      "idEndSuccess": null,
      "vehicleName": null,
      "vehicleStart": null,
      "vehicleEnd": null,
      "vehicleNum": null,
      "vehicleAddress": null,
      "vehicleType": null,
      "vehicleFaceSuccess": null,
      "archiveNo": null,
      "vehicleEndSuccess": null,
      "authority": null,
      "birthdayPlace": null,
      "passCountry": null,
      "passExpiryDate": null,
      "passIssueDate": null,
      "passIssuePlace": null,
      "passName": null,
      "passportNum": null,
      "passPersonId": null,
      "licenseImgFrontName": null,
      "licenseImgFront": null,
      "licenseImgBackName": null,
      "licenseImgBack": null,
      "licenseImgHandheldName": null,
      "licenseImgHandheld": null,
      "licenceType": "IDENTITY",
      "verifyStatus": "PENDING",
      "createdBy": "",
      "createdDate": "2018-09-09T15:12:39Z",
      "lastModifiedBy": null,
      "lastModifiedDate": null
    }
    ```

#### 3.KYC C3 审核

```
GET    http://localhost:8080/user/approve/kyc-three-status/1/PENDING
```

* **接口说明：**
  * 目前 **C3** 审核暂无生物识别，所以用户一键申请后，后台获取的状态一般为 **PENDING**
* 参数说明：
  * Long userId
  * String **PENDING / PASSED / REJECTED**
* 返回结果：
  * ```
    {
      "id": 1,
      "userId": 1,
      "verifyStatus": "PENDING",
      "createdBy": "",
      "createdDate": "2018-09-09T11:42:47Z",
      "lastModifiedBy": null,
      "lastModifiedDate": "2018-09-09T11:42:47Z"
    }
    ```



