#### 1.输入 ids 查询用户信息

```
GET    http://localhost:8080/user/ids/1,2,3,4,5
```

* **接口使用说明：**
  * 传入 userId 数组，只返回 User 信息和用户相关权限
* 参数说明：
  * Long\[ \] :
* 返回结果：
  * ```
    [
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
        "lastModifiedBy": "system",
        "lastModifiedDate": null,
        "authorities": [
          "ROLE_USER",
          "ROLE_ADMIN"
        ]
      },
      {
        "id": 2,
        "email": "anonymous@localhost.com",
        "mobile": "+86-10009",
        "inkId": "1009",
        "areaCode": "+86",
        "firstName": "Anonymous",
        "lastName": "User",
        "imageUrl": "",
        "activated": true,
        "langKey": "en",
        "createdBy": "system",
        "createdDate": "2018-09-08T15:49:48Z",
        "lastModifiedBy": "system",
        "lastModifiedDate": null,
        "authorities": []
      },
      {
        "id": 3,
        "email": "admin@localhost.com",
        "mobile": "+86-10010",
        "inkId": "1010",
        "areaCode": "+86",
        "firstName": "Administrator",
        "lastName": "Administrator",
        "imageUrl": "",
        "activated": true,
        "langKey": "en",
        "createdBy": "system",
        "createdDate": "2018-09-08T15:49:48Z",
        "lastModifiedBy": "system",
        "lastModifiedDate": null,
        "authorities": [
          "ROLE_USER",
          "ROLE_ADMIN"
        ]
      },
      {
        "id": 4,
        "email": "user@localhost.com",
        "mobile": "+86-10086",
        "inkId": "1086",
        "areaCode": "+86",
        "firstName": "User",
        "lastName": "User",
        "imageUrl": "",
        "activated": true,
        "langKey": "en",
        "createdBy": "system",
        "createdDate": "2018-09-08T15:49:48Z",
        "lastModifiedBy": "system",
        "lastModifiedDate": null,
        "authorities": [
          "ROLE_USER"
        ]
      },
      {
        "id": 5,
        "email": "32694110@qq.com",
        "mobile": "+86-17610016050",
        "inkId": "10089",
        "areaCode": "+86",
        "firstName": "Gong",
        "lastName": "Tao",
        "imageUrl": null,
        "activated": true,
        "langKey": "zh-CN",
        "createdBy": "",
        "createdDate": "2018-09-08T15:53:01Z",
        "lastModifiedBy": null,
        "lastModifiedDate": "2018-09-09T19:53:42Z",
        "authorities": [
          "ROLE_USER",
          "ROLE_ADMIN"
        ]
      }
    ]
    ```



