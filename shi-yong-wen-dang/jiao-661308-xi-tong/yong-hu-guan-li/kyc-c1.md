#### KYC  C1 用户基本信息

```
GET    http://localhost:8080/user/pagination/kyc-one?page=0&size=5&sort=id
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
          "status1": "PENDING",
          "createdDate1": "2018-09-09T12:23:17Z",
          "lastModifiedDate1": "2018-09-10T15:29:26Z"
        },
        {
          "id": 2,
          "email": "anonymous@localhost.com",
          "mobile": "+86-10009",
          "type": "IDENTITY",
          "status1": "PASSED",
          "createdDate1": "2018-09-02T15:55:50Z",
          "lastModifiedDate1": "2018-09-08T15:55:33Z"
        },
        {
          "id": 3,
          "email": "admin@localhost.com",
          "mobile": "+86-10010",
          "type": "IDENTITY",
          "status1": "REJECTED",
          "createdDate1": "2018-09-03T15:56:01Z",
          "lastModifiedDate1": "2018-09-08T15:55:33Z"
        },
        {
          "id": 4,
          "email": "user@localhost.com",
          "mobile": "+86-10086",
          "type": "IDENTITY",
          "status1": "PENDING",
          "createdDate1": "2018-09-04T15:56:28Z",
          "lastModifiedDate1": "2018-09-08T15:55:33Z"
        },
        {
          "id": 5,
          "email": "32694110@qq.com",
          "mobile": "+86-17610016050",
          "type": "IDENTITY",
          "status1": "PASSED",
          "createdDate1": "2018-09-09T15:20:27Z",
          "lastModifiedDate1": "2018-09-09T15:20:27Z"
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



