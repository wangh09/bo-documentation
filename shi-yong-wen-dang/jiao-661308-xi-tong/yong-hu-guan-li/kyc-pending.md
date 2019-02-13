#### KYC 所有认证未通过的用户基本信息

```
GET    http://localhost:8080/user/pagination/kyc-pending?page=0&size=5&sort=id
```

* 参数说明：参考分页说明
* 返回结果：
  * ```
    {
      "content": [
        {
          "id": 1,
          "email": "system@localhost.com",
          "mobile": "+86-10000",
          "createdDate": "2018-09-08T15:49:48Z",
          "type": "IDENTITY",
          "status1": "PENDING",
          "createdDate1": "2018-09-09T12:23:17Z",
          "lastModifiedDate1": "2018-09-10T15:29:26Z",
          "status2": "PASSED",
          "createdDate2": "2018-09-09T15:12:39Z",
          "lastModifiedDate2": null,
          "getStatus3": null,
          "createdDate3": "2018-09-09T11:42:47Z",
          "lastModifiedDate3": "2018-09-09T11:42:47Z"
        },
        {
          "id": 2,
          "email": "anonymous@localhost.com",
          "mobile": "+86-10009",
          "createdDate": "2018-09-08T15:49:48Z",
          "type": "IDENTITY",
          "status1": "PASSED",
          "createdDate1": "2018-09-02T15:55:50Z",
          "lastModifiedDate1": "2018-09-08T15:55:33Z",
          "status2": "PASSED",
          "createdDate2": "2018-09-08T15:57:36Z",
          "lastModifiedDate2": "2018-09-08T15:55:33Z",
          "getStatus3": null,
          "createdDate3": "2018-09-08T15:58:49Z",
          "lastModifiedDate3": "2018-09-08T15:55:33Z"
        },
        {
          "id": 5,
          "email": "32694110@qq.com",
          "mobile": "+86-17610016050",
          "createdDate": "2018-09-08T15:53:01Z",
          "type": "IDENTITY",
          "status1": "PASSED",
          "createdDate1": "2018-09-09T15:20:27Z",
          "lastModifiedDate1": "2018-09-09T15:20:27Z",
          "status2": "PASSED",
          "createdDate2": "2018-09-08T15:58:26Z",
          "lastModifiedDate2": "2018-09-08T15:55:33Z",
          "getStatus3": null,
          "createdDate3": "2018-09-08T15:59:17Z",
          "lastModifiedDate3": "2018-09-08T15:55:33Z"
        },
        {
          "id": 10,
          "email": "17610600736@163.com",
          "mobile": "+86-17610600736",
          "createdDate": "2018-09-09T19:01:46Z",
          "type": "IDENTITY",
          "status1": "PASSED",
          "createdDate1": "2018-09-10T03:40:04Z",
          "lastModifiedDate1": "2018-09-10T03:40:04Z",
          "status2": null,
          "createdDate2": null,
          "lastModifiedDate2": null,
          "getStatus3": null,
          "createdDate3": null,
          "lastModifiedDate3": null
        }
      ],
      "number": 0,
      "size": 5,
      "totalElements": 4,
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
      "numberOfElements": 4
    }
    ```



