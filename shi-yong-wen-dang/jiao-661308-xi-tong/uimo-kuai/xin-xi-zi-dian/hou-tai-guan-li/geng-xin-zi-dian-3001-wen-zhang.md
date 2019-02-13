#### 1.添加 / 更新 字典、文章

```
POST    http://localhost:8080/manager/info/dict
```

* **接口参数说明：若只创建字典项，文章内容数据不填。必须默认语种一次性创建。**

  * **创建 ：**

    * **dictionary ：依据参数说明**

      * **parent 和 name 必须是英文，且多语种状态下都相同，并且 name 允许同语种重复，否则添加时抛出500错误。**

    * * **如果是公告详情，则 content 的 title 必须补填到 dictionary 的 description 中。方便在公告详情分页展示文章内容。**
    * **content ：必填参数**

      * title

      * content

      * language

      * isShow

      * orderBy

  * **更新 ：补填参数**

    * **dictionary ：主键 **
    * **content ：**
      * **主键**
      * **dicId**
      * **uniqueId**

* 参数说明：

  * ```
    [
      {
        "contentDTO": {
          "content": "test",
          "isShow": true,
          "language": "zh-CN",
          "orderBy": 0,
          "title": "test"
        },
        "dictionaryDTO": {
          "description": "test",
          "isShow": true,
          "language": "zh-CN",
          "name": "test",
          "orderBy": 0,
          "parent": "notice",
          "status": 0
        }
      },
      {
        "contentDTO": {
          "content": "testEN",
          "isShow": true,
          "language": "en-US",
          "orderBy": 0,
          "title": "testEN"
        },
        "dictionaryDTO": {
          "description": "testEN",
          "isShow": true,
          "language": "en-US",
          "name": "test",
          "orderBy": 0,
          "parent": "notice",
          "status": 0
        }
      },
      {
        "contentDTO": {
          "content": "testKR",
          "isShow": true,
          "language": "ko-KR",
          "orderBy": 0,
          "title": "testKR"
        },
        "dictionaryDTO": {
          "description": "testKR",
          "isShow": true,
          "language": "ko-KR",
          "name": "test",
          "orderBy": 0,
          "parent": "notice",
          "status": 0
        }
      },
      {
        "contentDTO": {
          "content": "testJP",
          "isShow": true,
          "language": "ja-JP",
          "orderBy": 0,
          "title": "testJP"
        },
        "dictionaryDTO": {
          "description": "testJP",
          "isShow": true,
          "language": "ja-JP",
          "name": "test",
          "orderBy": 0,
          "parent": "notice",
          "status": 0
        }
      }
    ]
    ```

* **返回结果：**

  * ```
    [
      {
        "dictionaryDTO": {
          "id": 204,
          "parent": "notice",
          "name": "test",
          "language": "zh-CN",
          "isShow": true,
          "url": null,
          "imgUrl": null,
          "status": 0,
          "orderBy": 0,
          "description": "test",
          "extension": null,
          "createdBy": "1111111111111111111111111111",
          "createdDate": "2018-08-15T15:06:59.180Z",
          "lastModifiedBy": "1111111111111111111111111111",
          "lastModifiedDate": "2018-08-15T15:06:59.180Z"
        },
        "contentDTO": {
          "id": 131,
          "dicId": 204,
          "uniqueId": "6628893e70144205a16fda2ed59c42ce",
          "title": "test",
          "description": null,
          "extension": null,
          "content": "test",
          "isShow": true,
          "language": "zh-CN",
          "orderBy": 0,
          "createdBy": "1111111111111111111111111111",
          "createdDate": "2018-08-15T15:06:59.318Z",
          "lastModifiedBy": "1111111111111111111111111111",
          "lastModifiedDate": "2018-08-15T15:06:59.318Z"
        }
      },
      {
        "dictionaryDTO": {
          "id": 205,
          "parent": "notice",
          "name": "test",
          "language": "en-US",
          "isShow": true,
          "url": null,
          "imgUrl": null,
          "status": 0,
          "orderBy": 0,
          "description": "testEN",
          "extension": null,
          "createdBy": "1111111111111111111111111111",
          "createdDate": "2018-08-15T15:06:59.414Z",
          "lastModifiedBy": "1111111111111111111111111111",
          "lastModifiedDate": "2018-08-15T15:06:59.414Z"
        },
        "contentDTO": {
          "id": 132,
          "dicId": 205,
          "uniqueId": "d0dddaf6bde64099964fb47ae7b9ef54",
          "title": "testEN",
          "description": null,
          "extension": null,
          "content": "testEN",
          "isShow": true,
          "language": "en-US",
          "orderBy": 0,
          "createdBy": "1111111111111111111111111111",
          "createdDate": "2018-08-15T15:06:59.501Z",
          "lastModifiedBy": "1111111111111111111111111111",
          "lastModifiedDate": "2018-08-15T15:06:59.501Z"
        }
      },
      {
        "dictionaryDTO": {
          "id": 206,
          "parent": "notice",
          "name": "test",
          "language": "ko-KR",
          "isShow": true,
          "url": null,
          "imgUrl": null,
          "status": 0,
          "orderBy": 0,
          "description": "testKR",
          "extension": null,
          "createdBy": "1111111111111111111111111111",
          "createdDate": "2018-08-15T15:06:59.621Z",
          "lastModifiedBy": "1111111111111111111111111111",
          "lastModifiedDate": "2018-08-15T15:06:59.621Z"
        },
        "contentDTO": {
          "id": 133,
          "dicId": 206,
          "uniqueId": "4c6f508f0e5f491fb569cf549b333612",
          "title": "testKR",
          "description": null,
          "extension": null,
          "content": "testKR",
          "isShow": true,
          "language": "ko-KR",
          "orderBy": 0,
          "createdBy": "1111111111111111111111111111",
          "createdDate": "2018-08-15T15:06:59.688Z",
          "lastModifiedBy": "1111111111111111111111111111",
          "lastModifiedDate": "2018-08-15T15:06:59.688Z"
        }
      },
      {
        "dictionaryDTO": {
          "id": 207,
          "parent": "notice",
          "name": "test",
          "language": "ja-JP",
          "isShow": true,
          "url": null,
          "imgUrl": null,
          "status": 0,
          "orderBy": 0,
          "description": "testJP",
          "extension": null,
          "createdBy": "1111111111111111111111111111",
          "createdDate": "2018-08-15T15:06:59.776Z",
          "lastModifiedBy": "1111111111111111111111111111",
          "lastModifiedDate": "2018-08-15T15:06:59.776Z"
        },
        "contentDTO": {
          "id": 134,
          "dicId": 207,
          "uniqueId": "2e1d9f6c2f744fe8bf6049286872b7f4",
          "title": "testJP",
          "description": null,
          "extension": null,
          "content": "testJP",
          "isShow": true,
          "language": "ja-JP",
          "orderBy": 0,
          "createdBy": "1111111111111111111111111111",
          "createdDate": "2018-08-15T15:06:59.831Z",
          "lastModifiedBy": "1111111111111111111111111111",
          "lastModifiedDate": "2018-08-15T15:06:59.831Z"
        }
      }
    ]
    ```

* **异常错误：**

  * **当 name 在同一语言重复时，抛出 500 错误。**



