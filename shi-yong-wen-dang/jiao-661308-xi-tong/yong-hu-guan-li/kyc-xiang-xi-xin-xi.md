#### KYC 用户详细信息

```
GET    http://localhost:8080/user/kyc-details/1
```

* **接口使用说明：**

  * **状态说明：**
    * **LicenceType    证件类型**
      * **IDENTITY    身份证**
      * **VEHICLE     驾驶证**
      * **PASSPORT    护照**
    * **VerifyStatus    认证状态**
      * **PENDING    认证中**
      * **PASSED    已通过**
      * **REJECTED    被拒绝**

* * **首先展示基本信息：**
    * ```
      Long userId    用户 ID
      String familyName    姓
      String givenName    名
      String countryName    国家名字
      LicenceType licenceType    认证类型
      VerifyStatus oneVerifyStatus    C1 的认证状态
      ```
  * 根据 **LicenceType** 展示不同的数据结构

    * C1 IDENTITY 数据
      * ```
        String sex                 性别：男  
        String idNum               身份证号：51112619951111111
        String realName            姓名：张三
        String birthday            出生年月：1995-11-11
        String province            省：四川省
        String city                市：乐山市
        String prefecture          区县：夹江县
        Boolean idSuccess          是否通过
        ```
    * C1 VEHICLE 数据

      * ```
        String vehicleName        
        String vehicleType        驾证级别：C1
        String vehicleStart       有效起始：2014-09-22 00:00:00
        String vehicleEnd         有效截止：2020-09-22 00:00:00
        String vehicleNum         驾证号码：32111****
        String archiveNo          档案号：511011***** 
        Boolean vehicleSuccess    是否通过
        ```

    * C1 PASSPROT 数据

      * ```
        String passportNum        护照号码：
        Boolean passSuccess
        ```

    * C2 IDENTITY 数据

      * ```
        # Face Data
        String sex                性别：男
        String birthday           出生日期：20000101
        String idAddress          地址：浙江省杭州市余杭区文一西路969号
        String idName             姓名：张三
        String nationality        民族：汉
        String idCardNum          身份证号：1234567890
        Boolean idFaceSuccess     识别结果：true / false

        # Back Data
        String startDate          有效起始：19700101
        String endDate            有效截止：19800101
        String issue              签发机关：杭州市公安局
        Boolean idEndSuccess      识别结果：true / false
        ```

    * C2 VEHICLE 数据

      * ```
        # Face Data
        String vehicleName
        String vehicleStart           有效起始：2010xxxx
        String vehicleEnd             有效截止：2010xxxx
        String vehicleNum             驾驶证号：360502xxxx03071357
        String vehicleAddress         地址：北京市海淀区清华园6号楼
        String vehicleType            驾证级别：C1
        Boolean vehicleFaceSuccess    识别结果：true / false

        # Back Data
        String archiveNo              档案编号：370211375349
        Boolean vehicleEndSuccess     识别结果：true / false
        ```

    * C2 PASSPORT 数据

      * ```
        # 护照只有 Face Data
        String authority            签发机关：公安部出入境管理局
        String birthdayPlace        出生地：广西
        String passCountry          国籍：CHN
        String passExpiryDate       到期日期：20230501
        String passIssueDate        发证日期：20130502
        String passIssuePlace       发证地址：广西
        String passName             护照姓名：WANG.JING
        String passportNum          护照号码：E20354xxxx
        String passPersonId         持照人身份ID：MNPELOLIOKLPA9
        ```

    * C2 OSS 数据

      * ```
        String licenseImgFrontName        正面照片名字，删除照片信息时，传入该值
        String licenseImgFront            正面照片自适应地址
        String licenseImgBackName         背面照片名字，删除照片信息时，传入该值
        String licenseImgBack             背面照片自适应地址
        String licenseImgHandheldName     手持照片名字，删除照片信息时，传入该值

        String licenseImgHandheld         手持照片自适应地址
        LicenceType licenceType           证件类型
        VerifyStatus verifyStatus         认证状态
        ```

    * C3 数据

      * ```
        VerifyStatus verifyStatus
        ```
* 参数说明：

  * int  userId :

* 返回结果：

  * ```
    {
      "userId": 1,
      "familyName": "Admin",
      "givenName": "admin",
      "countryName": "",
      "licenceType": "IDENTITY",
      "oneVerifyStatus": "PENDING",
      "oneIdentity": {
        "sex": null,
        "idNum": null,
        "realName": null,
        "birthday": null,
        "province": null,
        "city": null,
        "prefecture": null,
        "idSuccess": null
      },
      "oneVehicle": null,
      "onePassport": null,
      "twoIdentity": {
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
        "idEndSuccess": null
      },
      "twoVehicle": null,
      "twoPassport": null,
      "twoOcrInfo": null,
      "threeInfo": {
        "verifyStatus": "PENDING"
      }
    }
    ```

* 异常情况：

  * userId 不存在时，500错误。



