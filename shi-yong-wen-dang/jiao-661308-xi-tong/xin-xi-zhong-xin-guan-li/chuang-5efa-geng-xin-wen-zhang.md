#### 1.创建/更新文章

```
POST    http://localhost:8080/web-server/info/article
```

* **接口说明：默认语种必须一次性创建**

  * **Content 创建必填参数：**

    * **title、content、isShow、language、order 必填字段**

  * **Content 更新必填参数：**

    * **id**
    * **dicId**
    * **uniqueId （同一文字多语种拥有相同的 uniqueId）**

* **参数说明：**

```
[
    {
        ["id": 110,]
        ["dicId": 100,]
        ["uniqueId": "cd1b93b2a90a424f947fb352f774ac3d",]
        "title": "上币公告",
        "content": "***************",
        "language": "zh-CN",
        "isShow": true,
        "order": 1,
        "description": "上币公告中文说明",
        "extension": null
    },
    ......[en-US]、[ko-KR]、[ja-JP]
]
```

* **返回结果：**

```
[
    {
        "id": 110,
        "dicId": 100,
        "uniqueId": "cd1b93b2a90a424f947fb352f774ac3d",
        "title": "上币公告",
        "content": "***************",
        "language": "zh-CN",
        "isShow": true,
        "order": 1,
        "description": "上币公告中文说明",
        "extension": null,
        "createdBy": "anonymousUser",
        "createdDate": "2018-10-27T16:59:10.114Z",
        "lastModifiedBy": "anonymousUser",
        "lastModifiedDate": "2018-10-27T16:59:10.114Z"
    },
    ......[en-US]、[ko-KR]、[ja-JP]
]
```

* **异常情况：**
  * **424  Content 的 dicId 在新建时，已经重复。保证一个字典节点对应一篇文章（UI 模块 424 异常）**



