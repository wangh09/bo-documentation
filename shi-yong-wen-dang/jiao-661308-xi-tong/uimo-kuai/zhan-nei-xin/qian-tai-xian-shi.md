## 前台展示

---

#### 1.检查站内信

```
GET    http://localhost:8082/ui/message/check/new
```

* **接口说明：用户登录网站，或进入站内信页面前调用该接口，检查用户是否有未接收的信息**
* **返回结果：如果没有，返回 null。有则会显示未接收的所有信息。**
  * ```
    {
      "unreadCount": 1,
      "readCount": 0,
      "unreadCustomerList": [
        {
          "id": 146,
          "receiverId": 12,
          "msgId": 112,
          "messageStatus": "UNREAD",
          "messageType": "PUBLIC",
          "createdBy": "1111111111111111111111111111",
          "createdDate": "2018-08-14T03:15:33.006Z",
          "lastModifiedBy": "1111111111111111111111111111",
          "lastModifiedDate": "2018-08-14T03:15:33.006Z"
        }
      ],
      "readCustomerList": []
    }
    ```

#### 2.检查未读条数

```
GET    http://localhost:8082/ui/message/check/count
```

* **接口说明：如果 unreadCount + readCount ≠ totalCount ，可以计算用户删除的信息数量**

* 返回结果：

  * ```
    {
      "totalCount": 4,
      "unreadCount": 4,
      "readCount": 0
    }
    ```

### 3.显示用户信息

```
GET    http://localhost:8082/ui/message/view/{language}?page=0&size=5&sort=createdDate,desc
```

* 参数说明：
  * String  **language :  zh-CN / en-US / ko-KR / ja-JP**
  * **Pageable :**
    * Integer  **page : 0**
    * Integer  **size : 5**
    * **Sort  Array String   排序**
* 返回结果：
  * ```
    {
      "unreadList": [
        {
          "id": 146,
          "title": " 测试标题CN",
          "content": "站内信测试内容CN",
          "language": "zh-CN",
          "messageStatus": "UNREAD",
          "messageType": "PUBLIC",
          "createdBy": "1111111111111111111111111111",
          "createdDate": "2018-08-14T03:15:16Z",
          "lastModifiedBy": "1111111111111111111111111111",
          "lastModifiedDate": "2018-08-14T03:15:16Z"
        },
        {
          "id": 144,
          "title": " 测试标题-1CN-PUBLIC",
          "content": "站内信测试内容-1CN-PUBLIC",
          "language": "zh-CN",
          "messageStatus": "UNREAD",
          "messageType": "PUBLIC",
          "createdBy": "1111111111111111111111111111",
          "createdDate": "2018-08-13T16:29:52Z",
          "lastModifiedBy": "1111111111111111111111111111",
          "lastModifiedDate": "2018-08-13T16:29:52Z"
        },
        {
          "id": 143,
          "title": " 测试标题-1CN",
          "content": "站内信测试内容-1CN",
          "language": "zh-CN",
          "messageStatus": "UNREAD",
          "messageType": "PRIVATE",
          "createdBy": "1111111111111111111111111111",
          "createdDate": "2018-08-13T16:25:06Z",
          "lastModifiedBy": "1111111111111111111111111111",
          "lastModifiedDate": "2018-08-13T16:25:06Z"
        },
        {
          "id": 142,
          "title": "修改-测试标题CN",
          "content": "修改-站内信测试内容CN",
          "language": "zh-CN",
          "messageStatus": "UNREAD",
          "messageType": "PRIVATE",
          "createdBy": "1111111111111111111111111111",
          "createdDate": "2018-08-13T15:17:23Z",
          "lastModifiedBy": "1111111111111111111111111111",
          "lastModifiedDate": "2018-08-13T16:02:46Z"
        }
      ],
      "readList": []
    }
    ```

#### 4.更改信息为已读状态

```
PUT    http://localhost:8082/ui/message/view/{id}
```

* 参数说明：
  * **Long  id **
* 返回结果：
  * ```
    {
      "id": 142,
      "receiverId": 12,
      "msgId": 108,
      "messageStatus": "READ",
      "messageType": "PRIVATE",
      "createdBy": "1111111111111111111111111111",
      "createdDate": "2018-08-13T15:17:23Z",
      "lastModifiedBy": "1111111111111111111111111111",
      "lastModifiedDate": "2018-08-13T15:17:23Z"
    }
    ```

#### 5.物理删除信息

```
DELETE    http://localhost:8082/ui/message/delete/{id}
```

* **接口说明：该接口会物理删除信息，慎用。**
  * **check/new-message  接口默认以用户的最近一条信息时间（如果没有，以注册时间为节点）作为节点，检查用户未接收信息。所以如果删除了最近一条信息，则会出现 bug。**
  * **若使用该接口，可以将最近一条改为逻辑删除，其余的全部使用物理删除。**



