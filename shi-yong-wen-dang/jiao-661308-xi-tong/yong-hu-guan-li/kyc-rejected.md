#### 1.KYC 所有被拒绝的用户基本信息

```
GET    http://localhost:8080/user/pagination/kyc-rejected?page=0&size=5&sort=id
```

* 参数说明：见分页说明
* 返回结果：

  * ```
    {
      "content": [
        {
          "id": 3,
          "email": "admin@localhost.com",
          "mobile": "+86-10010",
          "createdDate": "2018-09-08T15:49:48Z",
          "type": "IDENTITY",
          "status1": "REJECTED",
          "createdDate1": "2018-09-03T15:56:01Z",
          "lastModifiedDate1": "2018-09-08T15:55:33Z",
          "status2": "REJECTED",
          "createdDate2": "2018-09-08T15:57:54Z",
          "lastModifiedDate2": "2018-09-08T15:55:33Z",
          "getStatus3": null,
          "createdDate3": "2018-09-08T15:58:55Z",
          "lastModifiedDate3": "2018-09-08T15:55:33Z"
        },
        {
          "id": 4,
          "email": "user@localhost.com",
          "mobile": "+86-10086",
          "createdDate": "2018-09-08T15:49:48Z",
          "type": "IDENTITY",
          "status1": "PENDING",
          "createdDate1": "2018-09-04T15:56:28Z",
          "lastModifiedDate1": "2018-09-08T15:55:33Z",
          "status2": "PENDING",
          "createdDate2": "2018-09-08T15:58:09Z",
          "lastModifiedDate2": "2018-09-08T15:55:33Z",
          "getStatus3": null,
          "createdDate3": "2018-09-08T15:59:08Z",
          "lastModifiedDate3": "2018-09-08T15:55:33Z"
        }
      ],
      "number": 0,
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
        "paged": true,
        "unpaged": false
      },
      "last": true,
      "totalPages": 1,
      "sort": {
        "sorted": false,
        "unsorted": true
      },
      "first": true,
      "numberOfElements": 2
    }
    ```

#### 2.删除用户 C2 OSS 照片

```
DELETE    http://localhost:8080/user/rejected/licence-img/87198916f64541e7a783287b91f608fe.png/bbdcc66de8f94b55886ebf119f6c8144.png/a2222f4fd9394d89b31ead300b1d7b7d.png
```

* **接口使用说明：**
  * 当 C2 审核拒绝后，调用该接口删除用户在 OSS 上的数据。
* 参数说明：
  * String frontName:
  * String backName:
  * String handheldName:
* 返回结果：
  * 无



