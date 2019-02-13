## KYC 认证

---

#### 1.KYC 全部基本信息

```
GET    http://localhost:8080/user/kyc/list/status?page={page}&size={size}&sort=[sort]
```

* **接口场景：**
  * **用户如果 KYC 没有认证，则 status1 / status2 / status3 为 nul**l
* * **用户实名认证，用户显示两种场景。（分页显示用户基本信息和 KYC 基本信息及认证状态）**
* **参数说明：**
  * **int page :** **0  \(起始页\)**
  * **int size ：5  （每页数量）**
  * **Array sort ：sort=id \(默认 id，正序排序\) ， sort=createdDate1,desc （默认用户 KYC 的 C1提交时间，倒序排序\)**
* **返回参数简要说明：**

  * totalPages ：总页码

  * totalElements ：总数量

  * first ：是否是第一页

  * last ：是否是最后一页

  * **createdDate :  用户注册时间**

  * **kycCreatedDate : KYC 首次认证时间。**

  * **authorityName ：用户的权限级别，如果是 ROLE\_FREEEZE 则证明该用户被冻结，暂时不能登录。**

* **返回结果：**

```
{
  "content": [
    {
      "id": 5,
      "email": "32694110@qq.com",
      "mobile": "+86-17610016050",
      "createdDate": "2018-09-08T15:53:01Z",
      "level": "normal",
      "status": "PASSED",
      "data": null,
      "extraData": null,
      "description": null,
      "extension": null,
      "kycCreatedDate": "2018-11-09T03:48:31Z",
      "kycLastModifiedDate": "2018-11-09T18:49:11Z",
      "authorityName": [
        "ROLE_ADMIN,ROLE_USER"
      ]
    },
    ......[other data]
  ],
  "size": 5,
  "totalElements": 2,
  "pageable": {
    "sort": {
      "sorted": false,
      "unsorted": true
    },
    "offset": 0,
    "pageSize": 5,
    "pageNumber": 0,
    "unpaged": false,
    "paged": true
  },
  "last": true,
  "totalPages": 1,
  "sort": {
    "sorted": false,
    "unsorted": true
  },
  "first": true,
  "numberOfElements": 2,
  "number": 0
}
```

* **异常情况：无**

#### 2.KYC未认证的用户信息

```
GET    http://localhost:8080/user/kyc/list/no-status?page={page}&size={size}&sort=[sort]
```

* **参数说明：**同上
* **返回结果：因为用户未认证，所以返回的是所有用户的基本信息**

```
{
  "content": [
    {
      "id": 1,
      "email": "system@localhost.com",
      "mobile": "+86-10000",
      "inkId": "1000",
      "areaCode": "+86",
      "firstName": "System",
      "lastName": "System",
      "imageUrl": "",
      "activated": true,
      "langKey": "en",
      "createdBy": "system",
      "createdDate": "2018-09-08T15:49:48Z",
      "lastModifiedBy": "anonymousUser",
      "lastModifiedDate": "2018-10-19T07:40:57Z",
      "authorities": [
        "ROLE_USER"
      ]
    },
    ......[other data]
  ],
  "size": 5,
  "totalElements": 29,
  "pageable": {
    "sort": {
      "sorted": false,
      "unsorted": true
    },
    "offset": 0,
    "pageSize": 5,
    "pageNumber": 0,
    "unpaged": false,
    "paged": true
  },
  "last": false,
  "totalPages": 6,
  "sort": {
    "sorted": false,
    "unsorted": true
  },
  "first": true,
  "numberOfElements": 5,
  "number": 0
}
```

* **异常情况：无**



