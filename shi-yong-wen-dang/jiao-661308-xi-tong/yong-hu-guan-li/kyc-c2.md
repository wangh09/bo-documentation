#### KYC C2 用户基本信息

```
GET    http://localhost:8080/user/pagination/kyc-two?page=0&size=5&sort=id
```

* 参数说明：见分页说明
* 返回结果：
  * ```
    {
      "content": [
        {
          "id": 1,
          "email": "system@localhost.com",
          "mobile": "+86-10000",
          "type": "IDENTITY",
          "status2": "PASSED",
          "createdDate2": "2018-09-09T15:12:39Z",
          "lastModifiedDate2": null
        },
        {
          "id": 2,
          "email": "anonymous@localhost.com",
          "mobile": "+86-10009",
          "type": "IDENTITY",
          "status2": "PASSED",
          "createdDate2": "2018-09-08T15:57:36Z",
          "lastModifiedDate2": "2018-09-08T15:55:33Z"
        },
        {
          "id": 3,
          "email": "admin@localhost.com",
          "mobile": "+86-10010",
          "type": "IDENTITY",
          "status2": "REJECTED",
          "createdDate2": "2018-09-08T15:57:54Z",
          "lastModifiedDate2": "2018-09-08T15:55:33Z"
        },
        {
          "id": 4,
          "email": "user@localhost.com",
          "mobile": "+86-10086",
          "type": "IDENTITY",
          "status2": "PENDING",
          "createdDate2": "2018-09-08T15:58:09Z",
          "lastModifiedDate2": "2018-09-08T15:55:33Z"
        },
        {
          "id": 5,
          "email": "32694110@qq.com",
          "mobile": "+86-17610016050",
          "type": "IDENTITY",
          "status2": "PASSED",
          "createdDate2": "2018-09-08T15:58:26Z",
          "lastModifiedDate2": "2018-09-08T15:55:33Z"
        }
      ],
      "number": 0,
      "size": 5,
      "totalElements": 9,
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
      "last": false,
      "totalPages": 2,
      "sort": {
        "sorted": false,
        "unsorted": true
      },
      "first": true,
      "numberOfElements": 5
    }
    ```



