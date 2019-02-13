#### 1.创建站内信分组用户

```
POST    http://localhost:8080/web-server/message/group
```

* **接口说明：一个分组内，receiverId 不会出现重复情况，如果该组已有成员，再次创建，默认更新本条数据。**
* **参数说明：**
  * Sting **groupName : 分组名称**
  * Long **receiverId : 站内信接收用户ID**
  * Boolean **isShow :  该组发送信息时，该用户是否接收。（如果用户设置 false 状态时，发送了一条分组站内信，当设置为 true 状态时，该用户并不会接收到该条站内信）**
  * String **descripttion : 描述**

```
[
  {
    "groupName": "LEVEL1",
    "receiverId": 5,
    "isShow": true,
    "description": "LEVEL1 use test"
  },
  ......[other member]
]
```

* **返回结果：**

```
[
  {
    "id": 47,
    "groupName": "LEVEL1",
    "receiverId": 5,
    "isShow": true,
    "description": "LEVEL1 use test",
    "createdBy": "anonymousUser",
    "createdDate": "2018-10-29T02:06:58.636Z",
    "lastModifiedBy": "anonymousUser",
    "lastModifiedDate": "2018-10-29T02:06:58.636Z"
  },
  ......[other data]
]
```

* **异常情况：无**

#### 2.查看站内信已有分组

```
GET    http://localhost:8080/web-server/message/group
```

* **参数：无**
* **返回结果：**

```
[
  "LEVEL10",
  "LEVEL1",
  "LEVEL2",
  "LEVEL3"
]
```

* **异常情况：无**

#### **3.分页查看分组内成员**

```
GET    http://localhost:8080/web-server/message/group/member?groupName={groupName}[&isShow={isShow}]&page={page}&size={size}&sort=[sort]
```

* **参数说明：**
  * String **groupName : 必填（分组名称）**
  * Boolean **isShow : 非必填（有值时，查询该组是否接收站内信的用户。无值时，默认查询该组所以用户）**
  * **Pageable 参数参考其他分页**
* **返回结果：**

```
{
  "content": [
    {
      "id": 32,
      "groupName": "LEVEL1",
      "receiverId": 19,
      "isShow": true,
      "description": "ZU",
      "createdBy": "anonymousUser",
      "createdDate": "2018-10-25T08:33:08Z",
      "lastModifiedBy": "anonymousUser",
      "lastModifiedDate": "2018-10-25T08:33:08Z"
    },
    ......[other data]
  ],
  "size": 5,
  "totalElements": 5,
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
  "last": true,
  "totalPages": 1,
  "sort": {
    "sorted": false,
    "unsorted": true
  },
  "first": true,
  "numberOfElements": 5,
  "number": 0
}
```

* 返回分页参数部分说明：
  * **size : 请求分页数量**
  * **totalElements : 查询到的总数**
  * **first : 是否是第一页**
  * **last : 是否是最后一页**
  * **numberOfElements : 当前页的数量**
* **异常情况：无**

#### 3.显示分组所有成员ID

```
GET    http://localhostt:8080/web-server/message/group/ids?groupName={groupName}[&isShow=true]
```

* **参数说明：**
  * String **groupName : 必填（分组名称）**
  * Boolean** isShow : 非必填（有值时，查询该组是否接收站内信的用户。无值时，默认查询该组所以用户）**
* **返回结果：**

```
[
  19,
  20,
  21,
  1,
  5
]
```

* **异常情况：无**

#### 4.批量删除分组用户

```
DELETE    http://localhost:8080/web-server/message/group/member/{groupName}/[Long]
```

* **参数说明：**
  * String** groupName : 分组名称**
  * Long **\[ \] : 该组成员 ID 数组 **
* **返回结果：**

```
“OK”
```

* **异常情况：无**

#### 5.删除分组

```
DELETE    http://localhost:8080/web-server/message/group/batch/{groupName}
```

* **参数说明：**
  * String **groupName : 分组名称**
* **返回结果：**

```
“OK”
```

* **异常情况：无**

#### 6.删除分组用户

```
DELETE    http://localhost:8080/web-server/message/group/member/{id}
```

* **参数说明：**
  * Long **id : 主键 id  （非 receiverId）**
* **返回结果：**

```
"OK"
```

* **异常情况：无**

#### 7.删除站内信

```
DELETE    http://localhost:8080/web-server/message/{messageId}
```

* **接口说明：根据 Message 主键 ID 删除，将删除站内信内容，并且在已经接收到该信息的用户列表中会消失。**
* **参数说明：**
  * Long **messageId**
* **返回结果：**

```
“OK”
```

* **异常情况：无**



