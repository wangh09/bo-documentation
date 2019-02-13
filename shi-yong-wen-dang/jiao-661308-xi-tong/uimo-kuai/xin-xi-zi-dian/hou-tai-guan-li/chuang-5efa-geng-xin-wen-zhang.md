#### 1.创建 / 更新文章内容

```
POST    http://localhost:8080/manager/info/article
```

* **接口说明：必须默认语种一次性创建**

  * **创建  ：**

    * **content : 必填参数**

      * title

      * content

      * **dicId  注意异常结果**

      * language

      * isShow

      * orderrBy

  * **更新：更新的内容从  **[http://localhost:8082/ui/info/manage/view/{parent}](http://localhost:8082/ui/info/manage/view/{parent})** 获取文章主键 id，dicId**

    * **content：补填 id**
    * **dicId 补填**
    * **uniqueId  相同内容的多语种值一样，根据 uniqueId 的值，将同一的文章放到一起编辑，更新，删除。**

* 参数说明：

  * ```
    [
      {
        "id": 127,
        "dicId": 13,
        "uniqueId": "d1b9ba339b4d4e4ab6263f35e3ff8fb1",
        "title": "创建 API 说明",
        "description": "创建 API 说明",
        "extension": "创建 API 说明",
        "content": "创建 API 说明",
        "isShow": true,
        "language": "zh-CN",
        "orderBy": 0,
        "createdBy": "1111111111111111111111111111",
        "createdDate": "2018-08-15T14:53:28.723Z",
        "lastModifiedBy": "1111111111111111111111111111",
        "lastModifiedDate": "2018-08-15T14:53:28.723Z"
      },
      {
        "id": 128,
        "dicId": 34,
        "uniqueId": "a38dd37a2da94df6a6c5e5efa1ffb6e0",
        "title": "创建 API 说明EN",
        "description": "创建 API 说明EN",
        "extension": "创建 API 说明EN",
        "content": "创建 API 说明EN",
        "isShow": true,
        "language": "en-US",
        "orderBy": 0,
        "createdBy": "1111111111111111111111111111",
        "createdDate": "2018-08-15T14:53:28.932Z",
        "lastModifiedBy": "1111111111111111111111111111",
        "lastModifiedDate": "2018-08-15T14:53:28.932Z"
      },
      {
        "id": 129,
        "dicId": 55,
        "uniqueId": "15880e34c6a441ad96e3158df9d5e945",
        "title": "创建 API 说明KR",
        "description": "创建 API 说明KR",
        "extension": "创建 API 说明KR",
        "content": "创建 API 说明KR",
        "isShow": true,
        "language": "ko-KR",
        "orderBy": 0,
        "createdBy": "1111111111111111111111111111",
        "createdDate": "2018-08-15T14:53:28.976Z",
        "lastModifiedBy": "1111111111111111111111111111",
        "lastModifiedDate": "2018-08-15T14:53:28.976Z"
      },
      {
        "id": 130,
        "dicId": 76,
        "uniqueId": "06632d25037346f39cf84bb111dd0572",
        "title": "创建 API 说明JP",
        "description": "创建 API 说明JP",
        "extension": "创建 API 说明JP",
        "content": "创建 API 说明JP",
        "isShow": true,
        "language": "ja-JP",
        "orderBy": 0,
        "createdBy": "1111111111111111111111111111",
        "createdDate": "2018-08-15T14:53:29.017Z",
        "lastModifiedBy": "1111111111111111111111111111",
        "lastModifiedDate": "2018-08-15T14:53:29.017Z"
      }
    ]
    ```

* 返回结果：

  * ```
    [
      {
        "id": 82,
        "dicId": 14,
        "title": "费率标准",
        "description": "费率标准",
        "extension": "费率标准",
        "content": "费率标准",
        "isShow": true,
        "language": "zh-CN",
        "orderBy": 0,
        "createdBy": "1111111111111111111111111111",
        "createdDate": "2018-08-13T14:17:30.335Z",
        "lastModifiedBy": "1111111111111111111111111111",
        "lastModifiedDate": "2018-08-13T14:17:30.335Z"
      },
      {
        "id": 83,
        "dicId": 35,
        "title": "费率标准EN",
        "description": "费率标准EN",
        "extension": "费率标准EN",
        "content": "费率标准EN",
        "isShow": true,
        "language": "en-US",
        "orderBy": 0,
        "createdBy": "1111111111111111111111111111",
        "createdDate": "2018-08-13T14:17:30.363Z",
        "lastModifiedBy": "1111111111111111111111111111",
        "lastModifiedDate": "2018-08-13T14:17:30.363Z"
      },
      {
        "id": 84,
        "dicId": 56,
        "title": "费率标准KR",
        "description": "费率标准KR",
        "extension": "费率标准KR",
        "content": "费率标准KR",
        "isShow": true,
        "language": "ko-KR",
        "orderBy": 0,
        "createdBy": "1111111111111111111111111111",
        "createdDate": "2018-08-13T14:17:30.388Z",
        "lastModifiedBy": "1111111111111111111111111111",
        "lastModifiedDate": "2018-08-13T14:17:30.388Z"
      },
      {
        "id": 85,
        "dicId": 77,
        "title": "费率标准JP",
        "description": "费率标准JP",
        "extension": "费率标准JP",
        "content": "费率标准JP",
        "isShow": true,
        "language": "ja-JP",
        "orderBy": 0,
        "createdBy": "1111111111111111111111111111",
        "createdDate": "2018-08-13T14:17:30.412Z",
        "lastModifiedBy": "1111111111111111111111111111",
        "lastModifiedDate": "2018-08-13T14:17:30.412Z"
      }
    ]
    ```

* **异常说明：**

  * **当 content 的 dicId 已经存在于数据库，会抛出500异常。**



