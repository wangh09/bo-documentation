#### 1.分页查看站内信

```
GET    http://localhost:8080/web-server/message/view?page={page}&size={size}&sort=[sort]
```

* **接口说明：相同 msgTextId （相同内容）的多语种信息为一条，即 size 请求数量实际是  size \* 多语种**

  * **列表显示：同一 msgTextId 必须同时创建 / 更新 以保持数据同步**

* **参数说明：**

  * **Pageable：**
    * Integer **page : 0**
    * Integer** size : 5**
    * **Array sort : id,desc**

* **返回结果：**

```
{
    "totalPages": 1,
    "totalElements": 3,
    "first": true,
    "last": true,
    "sendList": [
        {
            "msgId": 110,
            "senderId": "m-01",
            "type": "PUBLIC",
            "receiverArray": null,
            "groupName": null,
            "textList": [
                {
                    "id": 217,
                    "msgTextId": "007f8c043f2741a48f24ed459533f3a1",
                    "title": " 站内信测试",
                    "content": "站内信测试内容",
                    "language": "zh-CN",
                    "isShow": true,
                    "createdBy": "1111111111111111111111111111",
                    "createdDate": "2018-08-13T16:29:52Z",
                    "lastModifiedBy": "1111111111111111111111111111",
                    "lastModifiedDate": "2018-08-13T16:29:52Z"
                },
                ...... [en-US]、[ja-JP]、[ko-JR]
            ]
        },
        ...... [other data]
    ]
}
```

* **异常情况：无**

---

#### 2.模糊查询站内信内容

```
GET    http://localhost:8080/web-server/message/search/{title}/{start}/{end}?page={page}&size={size}&sort=[sort]
```

* **参数说明：**
  * String **title : \[ 模糊的站内信标题 \]**
  * Long **start : \[ 毫秒时间戳 \]**
  * Long **end : \[ 毫秒时间戳 \]**
  * **Pageable **
    * Integer **page**
    * Integer **size**
    * Array **sort : id,desc**
* **返回结果：**

```
{
  "content": [
    {
      "id": 1,
      "msgTextId": "fabaabdd2e8b4191bd6b40ef12208062",
      "title": "测试站内信",
      "content": "测试站内信",
      "language": "zh-CN",
      "isShow": true,
      "createdBy": "anonymousUser",
      "createdDate": "2018-10-25T10:00:47Z",
      "lastModifiedBy": "anonymousUser",
      "lastModifiedDate": "2018-10-25T10:00:47Z"
    },
    ......[other data]
  ],
  "size": 5,
  "totalElements": 7,
  "pageable": {
    "sort": {
      "sorted": false,
      "unsorted": true
    },
    "pageSize": 5,
    "pageNumber": 0,
    "offset": 0,
    "unpaged": false,
    "paged": true
  },
  "last": false,
  "totalPages": 2,
  "sort": {
    "sorted": false,
    "unsorted": true
  },
  "first": true,
  "numberOfElements": 5,
  "number": 0
}
```

* **返回分页部分参数说明：**
  * **size : 请求分页数量**
  * **totalElements : 查询到的总数**
  * **first : 是否是第一页**
  * **last : 是否是最后一页**
  * **numberOfElements : 当前页的数量**
* **异常情况：无**



