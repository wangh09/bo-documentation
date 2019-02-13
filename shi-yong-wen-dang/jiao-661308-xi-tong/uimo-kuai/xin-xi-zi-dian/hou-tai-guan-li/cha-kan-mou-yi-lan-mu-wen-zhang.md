#### 1.查看某一栏目下文章

```
GET    http://localhost:8080/manager/info/article/view/{parent}?page=0&size=30&sort=id
```

* **接口说明：**

  * **该接口返回数据，自动把相同的 uniqueId 放入一个 list .**

* 参数说明：

  * String **parent ：notice**
  * **Pageable : **

    * **integer  page :  0**
    * **integer  size :  4 \(必须为语种的倍数\)**

    * **sort  排序**

* 返回参数说明：

  * totalPages : 总页码

  * totalElements : 总数量

  * first ：是否为第一页

  * last ：是否为最后一页

* 返回结果：

  * ```
    {
      "totalPages": 1,
      "totalElements": 16,
      "first": null,
      "last": null,
      "contentDTOList": [
          {
            "id": 146,
            "dicId": 219,
            "uniqueId": "f8ae3a923ab5496fbde8924e47dc9c95",
            "title": "testJP",
            "description": null,
            "extension": null,
            "content": "testJP",
            "isShow": true,
            "language": "ja-JP",
            "orderBy": 0,
            "createdBy": "1111111111111111111111111111",
            "createdDate": "2018-08-15T15:37:32Z",
            "lastModifiedBy": "1111111111111111111111111111",
            "lastModifiedDate": "2018-08-15T15:37:32Z"
          },
          {
            "id": 145,
            "dicId": 218,
            "uniqueId": "f8ae3a923ab5496fbde8924e47dc9c95",
            "title": "testKR",
            "description": null,
            "extension": null,
            "content": "testKR",
            "isShow": true,
            "language": "ko-KR",
            "orderBy": 0,
            "createdBy": "1111111111111111111111111111",
            "createdDate": "2018-08-15T15:37:28Z",
            "lastModifiedBy": "1111111111111111111111111111",
            "lastModifiedDate": "2018-08-15T15:37:28Z"
          },
          {
            "id": 144,
            "dicId": 217,
            "uniqueId": "f8ae3a923ab5496fbde8924e47dc9c95",
            "title": "testEN",
            "description": null,
            "extension": null,
            "content": "testEN",
            "isShow": true,
            "language": "en-US",
            "orderBy": 0,
            "createdBy": "1111111111111111111111111111",
            "createdDate": "2018-08-15T15:36:54Z",
            "lastModifiedBy": "1111111111111111111111111111",
            "lastModifiedDate": "2018-08-15T15:36:54Z"
          },
          {
            "id": 143,
            "dicId": 216,
            "uniqueId": "f8ae3a923ab5496fbde8924e47dc9c95",
            "title": "test",
            "description": null,
            "extension": null,
            "content": "test",
            "isShow": true,
            "language": "zh-CN",
            "orderBy": 0,
            "createdBy": "1111111111111111111111111111",
            "createdDate": "2018-08-15T15:35:58Z",
            "lastModifiedBy": "1111111111111111111111111111",
            "lastModifiedDate": "2018-08-15T15:35:58Z"
          }
        ],
    }
    ```



