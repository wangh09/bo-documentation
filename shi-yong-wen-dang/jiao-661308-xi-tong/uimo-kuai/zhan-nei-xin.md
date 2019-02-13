#### 1.检查站内信

```
GET    http://localhost:8082/ui/message/check/new
```

* **接口使用说明：用户登录网站，或进入站内信页面前调用该接口，检查用户是否有未接收的信息**
* **返回结果：**

```
“OK”
```

* **异常情况：500  UI 模块调用 UAA 模块获取用户信息失败**

#### 2.检查未读条数

```
GET    http://localhost:8082/ui/message/check/count
```

* **接口说明：如果 unreadCount + readCount ≠ totalCount ，可以计算用户删除的信息数量**

* **返回结果：**

```
{
  "totalCount": 11,
  "unreadCount": 2,
  "readCount": 9
}
```

* **异常情况：500  UI 模块调用 UAA 模块获取用户信息失败**

#### 3.显示用户站内信

```
GET    http://localhost:8082/ui/message/view/{language}?page={page}&size={size}&sort=[sort]
```

* **接口说明：**
  * **默认先显示所有的 unread 数据，并且按照 createdDate 倒序排序，然后再显示 read 数据，并且按照 lastModifiedDate 倒序排序。**
* **参数说明：**
  * String  **language :  zh-CN / en-US / ko-KR / ja-JP**
  * **Pageable :**
    * Integer  **page : 0**
    * Integer  **size : 5**
    * **Array sort : id,desc**
* **返回结果：**

```
{
  "unreadList": [
    {
      "id": 8,
      "title": "站内信测试",
      "content": "站内信测试第一条",
      "language": "zh-CN",
      "messageStatus": "UNREAD",
      "messageType": "PUBLIC",
      "createdBy": "10089",
      "createdDate": "2018-10-30T13:05:18Z",
      "lastModifiedBy": "10089",
      "lastModifiedDate": "2018-10-28T13:05:18Z"
    },
    ......[other data]
  ],
  "readList": []
}
```

* **异常情况：500  UI 模块调用 UAA 模块获取用户信息失败**

#### 4.更改信息为已读状态

```
PUT    http://localhost:8082/ui/message/view/{ids}
```

* **参数说明：**
  * **Long \[ \] ids **
* **返回结果：**

```
[
  {
    "id": 6,
    "receiverId": 5,
    "msgId": 2,
    "messageStatus": "READ",
    "messageType": "PRIVATE",
    "createdBy": "anonymousUser",
    "createdDate": "2018-10-28T12:56:20Z",
    "lastModifiedBy": "anonymousUser",
    "lastModifiedDate": "2018-10-28T12:56:20Z"
  },
  ......[other data]
]
```

* **异常情况：500  UI 模块调用 UAA 模块获取用户信息失败**

#### 5.更改信息为删除状态

```
PUT    http://localhost:8082/ui/message/delete/{ids}
```

* **参数说明：**
  * **Long \[ \] ids**
* **返回结果：**

```
[
  {
    "id": 6,
    "receiverId": 5,
    "msgId": 2,
    "messageStatus": "DELETE",
    "messageType": "PRIVATE",
    "createdBy": "anonymousUser",
    "createdDate": "2018-10-28T12:56:20Z",
    "lastModifiedBy": "10089",
    "lastModifiedDate": "2018-10-29T04:13:18Z"
  },
  ......[other data]
]
```

* **异常情况：500  UI 模块调用 UAA 模块获取用户信息失败**

#### 5.物理删除信息

```
DELETE    http://localhost:8082/ui/message/delete/{id}
```

* **接口说明：该接口会物理删除信息，慎用。**
  * **check/new-message  接口默认以用户的最近一条信息时间（如果没有，以注册时间为节点）作为节点，检查用户未接收信息。所以如果删除了最近一条信息，则会出现 bug。**
  * **若使用该接口，可以将最近一条改为逻辑删除，其余的全部使用物理删除。**
* **参数说明：**
  * Long **id : 用户站内信列表的 id**
* **返回结果：**

```
“OK”
```

* **异常情况：500  UI 模块调用 UAA 模块获取用户信息失败**



