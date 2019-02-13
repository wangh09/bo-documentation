#### 1.获取当前节点子节点\(多语种\)

```
GET    http://localhost:8082/ui/info/manage/list/{parent}
```

* **接口说明：**

  * **如果需要添加文章，调用该接口，根据相同的 name 获取不同语种的主键 id，作为 dicId 传入 content，创建多语种文章。**

* 参数说明：

  * String  **parent : notice**

* 返回结果：

  * ```
    [
      {
        "parent": "notice",
        "extension": null,
        "lastModifiedDate": null,
        "lastModifiedBy": null,
        "orderBy": 1,
        "description": "上币公告",
        "language": "zh-CN",
        "url": null,
        "isShow": true,
        "imgUrl": null,
        "createdDate": null,
        "createdBy": null,
        "name": "symbol",
        "id": 146
      },
      {
        "parent": "notice",
        "extension": null,
        "lastModifiedDate": null,
        "lastModifiedBy": null,
        "orderBy": 1,
        "description": "上币公告 EN",
        "language": "en-US",
        "url": null,
        "isShow": true,
        "imgUrl": null,
        "createdDate": null,
        "createdBy": null,
        "name": "symbol",
        "id": 147
      },
      {
        "parent": "notice",
        "extension": null,
        "lastModifiedDate": null,
        "lastModifiedBy": null,
        "orderBy": 1,
        "description": "上币公告 KR",
        "language": "ko-KR",
        "url": null,
        "isShow": true,
        "imgUrl": null,
        "createdDate": null,
        "createdBy": null,
        "name": "symbol",
        "id": 148
      },
      {
        "parent": "notice",
        "extension": null,
        "lastModifiedDate": null,
        "lastModifiedBy": null,
        "orderBy": 1,
        "description": "上币公告 JP",
        "language": "ja-JP",
        "url": null,
        "isShow": true,
        "imgUrl": null,
        "createdDate": null,
        "createdBy": null,
        "name": "symbol",
        "id": 149
      },
      {
        "parent": "notice",
        "extension": null,
        "lastModifiedDate": null,
        "lastModifiedBy": null,
        "orderBy": 0,
        "description": "提现公告",
        "language": "zh-CN",
        "url": null,
        "isShow": true,
        "imgUrl": null,
        "createdDate": null,
        "createdBy": null,
        "name": "tixiangonggao",
        "id": 150
      },
      {
        "parent": "notice",
        "extension": null,
        "lastModifiedDate": null,
        "lastModifiedBy": null,
        "orderBy": 0,
        "description": "提现公告EN",
        "language": "en-US",
        "url": null,
        "isShow": true,
        "imgUrl": null,
        "createdDate": null,
        "createdBy": null,
        "name": "tixiangonggao",
        "id": 151
      },
      {
        "parent": "notice",
        "extension": null,
        "lastModifiedDate": null,
        "lastModifiedBy": null,
        "orderBy": 0,
        "description": "提现公告KR",
        "language": "ko-KR",
        "url": null,
        "isShow": true,
        "imgUrl": null,
        "createdDate": null,
        "createdBy": null,
        "name": "tixiangonggao",
        "id": 152
      },
      {
        "parent": "notice",
        "extension": null,
        "lastModifiedDate": null,
        "lastModifiedBy": null,
        "orderBy": 0,
        "description": "项目公告--1",
        "language": "zh-CN",
        "url": null,
        "isShow": true,
        "imgUrl": null,
        "createdDate": null,
        "createdBy": null,
        "name": "xiangmugonggao",
        "id": 184
      },
      {
        "parent": "notice",
        "extension": null,
        "lastModifiedDate": null,
        "lastModifiedBy": null,
        "orderBy": 0,
        "description": "提现公告JP",
        "language": "ja-JP",
        "url": null,
        "isShow": true,
        "imgUrl": null,
        "createdDate": null,
        "createdBy": null,
        "name": "tixiangonggao",
        "id": 153
      },
      {
        "parent": "notice",
        "extension": null,
        "lastModifiedDate": null,
        "lastModifiedBy": null,
        "orderBy": 0,
        "description": "项目公告EN--1",
        "language": "en-US",
        "url": null,
        "isShow": true,
        "imgUrl": null,
        "createdDate": null,
        "createdBy": null,
        "name": "xiangmugonggao",
        "id": 185
      },
      {
        "parent": "notice",
        "extension": null,
        "lastModifiedDate": null,
        "lastModifiedBy": null,
        "orderBy": 0,
        "description": "项目公告",
        "language": "zh-CN",
        "url": null,
        "isShow": true,
        "imgUrl": null,
        "createdDate": null,
        "createdBy": null,
        "name": "项目公告",
        "id": 154
      },
      {
        "parent": "notice",
        "extension": null,
        "lastModifiedDate": null,
        "lastModifiedBy": null,
        "orderBy": 0,
        "description": "项目公告KR--1",
        "language": "ko-KR",
        "url": null,
        "isShow": true,
        "imgUrl": null,
        "createdDate": null,
        "createdBy": null,
        "name": "xiangmugonggao",
        "id": 186
      },
      {
        "parent": "notice",
        "extension": null,
        "lastModifiedDate": null,
        "lastModifiedBy": null,
        "orderBy": 0,
        "description": "项目公告EN",
        "language": "en-US",
        "url": null,
        "isShow": true,
        "imgUrl": null,
        "createdDate": null,
        "createdBy": null,
        "name": "项目公告EN",
        "id": 155
      },
      {
        "parent": "notice",
        "extension": null,
        "lastModifiedDate": null,
        "lastModifiedBy": null,
        "orderBy": 0,
        "description": "项目公告JP--1",
        "language": "ja-JP",
        "url": null,
        "isShow": true,
        "imgUrl": null,
        "createdDate": null,
        "createdBy": null,
        "name": "xiangmugonggao",
        "id": 187
      },
      {
        "parent": "notice",
        "extension": null,
        "lastModifiedDate": null,
        "lastModifiedBy": null,
        "orderBy": 0,
        "description": "项目公告KR",
        "language": "ko-KR",
        "url": null,
        "isShow": true,
        "imgUrl": null,
        "createdDate": null,
        "createdBy": null,
        "name": "项目公告KR",
        "id": 156
      },
      {
        "parent": "notice",
        "extension": null,
        "lastModifiedDate": null,
        "lastModifiedBy": null,
        "orderBy": 0,
        "description": "项目公告JP",
        "language": "ja-JP",
        "url": null,
        "isShow": true,
        "imgUrl": null,
        "createdDate": null,
        "createdBy": null,
        "name": "项目公告JP",
        "id": 157
      }
    ]
    ```



