## 后台管理

---

#### 3.删除站内信

```
DELETE    http://localhost:8080/manager/message/{messageId}
```

* 接口说明：**messageId  从** [http://localhost:8082/ui/manager/show/all-message](http://localhost:8082/ui/manager/show/all-message)** 获取**

  * **该接口为超级管理员操作，慎用。会删除用户已经收到的站内信。**

* 参数说明：

  * Long  **messageId :**

* 返回参数：

  * ```
    "OK"
    ```

#### 4.创建组

```
POST    http://localhost:8080/manager/message/group
```

* **接口说明：**

  * **目前显示业务层用户基本信息（邮箱、电话），可扩展 KYC 信息，底层账户交易流水信息（LEVEL）**

  * **用户信息单独调用分页接口，勾选相关用户到该组**

  * **同一组不允许重复用户，否则 500 异常**

* 参数说明：

  * ```
    [
      {
        "description": "LEVEL1 组",
        "groupName": "LEVEL1",
        "isShow": true,
        "receiverId": 12
      },
     {
        "description": "LEVEL1 组",
        "groupName": "LEVEL1",
        "isShow": true,
        "receiverId": 38
      }
    ]
    ```

* 返回结果：

  * ```
    [
      {
        "id": 34,
        "groupName": "LEVEL1",
        "receiverId": 12,
        "isShow": true,
        "description": "LEVEL1 组",
        "createdBy": "anonymousUser",
        "createdDate": "2018-08-13T16:41:42.956Z",
        "lastModifiedBy": "anonymousUser",
        "lastModifiedDate": "2018-08-13T16:41:42.956Z"
      },
      {
        "id": 35,
        "groupName": "LEVEL1",
        "receiverId": 38,
        "isShow": true,
        "description": "LEVEL1 组",
        "createdBy": "anonymousUser",
        "createdDate": "2018-08-13T16:41:43.008Z",
        "lastModifiedBy": "anonymousUser",
        "lastModifiedDate": "2018-08-13T16:41:43.008Z"
      }
    ]
    ```

#### 5.查看分组

```
GET    http://localhost:8080/manager/message/group
```

* 返回结果：
  * ```
    [
      "LEVEL4",
      "LEVEL5",
      "LEVEL6",
      "LEVEL7",
      "LEVEL1",
      "LEVEL2",
      "LEVEL3"
    ]
    ```

#### 6.获取所有组成员

```
GET    http://localhost:8080/manager/message/group/member?groupName=LEVEL1[&isShow=false]&page=0&size=5&sort=id
```

* **接口说明：当 isShow 传值时，则显示该组两种状态的成员。false 状态下的成员，不会收到站内信。**

* 参数说明：

  * String  ** groupName ： LEVEL1**
  * Boolean **isShow：true / false **
  * **Pageable : **

    * **Integer  page : 0**

    * **Integer  size : 5**

    * **Sort  Array  String  排序**

* 返回结果：

  * ```
    {
      "content": [
        {
          "id": 34,
          "groupName": "LEVEL1",
          "receiverId": 12,
          "isShow": true,
          "description": "LEVEL3 组",
          "createdBy": "1111111111111111111111111111",
          "createdDate": "2018-08-13T16:41:43Z",
          "lastModifiedBy": "1111111111111111111111111111",
          "lastModifiedDate": "2018-08-13T16:46:54Z"
        },
        {
          "id": 35,
          "groupName": "LEVEL1",
          "receiverId": 38,
          "isShow": true,
          "description": "LEVEL3 组",
          "createdBy": "1111111111111111111111111111",
          "createdDate": "2018-08-13T16:41:43Z",
          "lastModifiedBy": "1111111111111111111111111111",
          "lastModifiedDate": "2018-08-13T16:46:54Z"
        }
      ],
      "last": true,
      "totalElements": 2,
      "totalPages": 1,
      "size": 5,
      "number": 0,
      "sort": null,
      "first": true,
      "numberOfElements": 2
    }
    ```

#### 8.从该组删除成员

```
DELETE    http://localhost:8080/manager/message/group/member/{id}
```

* 参数说明：
  * **Long  id :  主键**
* 返回结果：
  * ```
    "OK"
    ```

#### 9.删除该组所有成员

```
DELETE    http://localhost:8080/manager/message/group/batch/{groupName}
```

* 参数说明：
  * String  **groupName : LEVEL5**
* 返回结果：
  * ```
    "OK"
    ```



