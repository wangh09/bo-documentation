#### 1.获取底层权限

```
GET    http://localhost:8080/manager/users/authorities
```

* **返回结果：**

```
[
  "ROLE_ADMIN",
  "ROLE_COIN",
  "ROLE_COIN_SYMBOL",
  "ROLE_COIN_TOKEN",
  ......[other data]
]
```

* **异常情况：无**

#### 2.创建、修改角色

```
POST    http://localhost:8080/manager/users/roles
```

* **接口使用说明：更新角色信息，如果有用户为该角色，则当前用户的角色名称会更新会最新的，底层权限也会随之更新。**
* **参数说明：**
  * **String roleName : **唯一性
  * **String authorityName : **使用 , 拼接底层权限

```
{
  ["id":5]
  "authorityName": "ROLE_ADMIN,ROLE_USER",
  "roleName": "SUPPORT"
}
```

* **返回结果：**

```
{
  "id": 5,
  "roleName": "SUPPORT",
  "authorityName": "ROLE_ADMIN,ROLE_USER"
}
```

* **异常情况：**
  * **400 更新的 id 不存在**
  * **500 roleName 必须是唯一，不允许重复**

#### 3.获取所有角色

```
GET    http://localhost:8080/manager/users/roles?page=[page]&size=[size]&sort=[sort]
```

* **参数说明：参考其他分页**
* **返回结果：**

```
{
  "content": [
    {
      "id": 1,
      "roleName": "ADMIN",
      "authorityName": "ROLE_ADMIN,ROLE_USER"
    },
    ......[other data]
  ],
  "pageable": {
    "sort": {
      "sorted": true,
      "unsorted": false
    },
    "offset": 0,
    "pageSize": 5,
    "pageNumber": 0,
    "paged": true,
    "unpaged": false
  },
  "last": true,
  "totalElements": 3,
  "totalPages": 1,
  "size": 5,
  "number": 0,
  "first": true,
  "sort": {
    "sorted": true,
    "unsorted": false
  },
  "numberOfElements": 3
}
```

* **异常情况：无**

#### 4.查看角色的底层权限

```
GET    http://localhost:8080/manager/users/roles/{roleName}
```

* **参数说明：**
  * **String roleName : **ADMIN
* **返回结果：**

```
{
  "id": 1,
  "roleName": "ADMIN",
  "authorityName": "ROLE_ADMIN,ROLE_USER"
}
```

* **异常情况：无**

#### 5.删除角色

```
DELETE    http://localhost:8080/manager/users/roles/{id}
```

* **参数说明：**
  * **Long id ：**分页中获取 id
* **返回结果：**

```
”OK“
```

* **异常情况：无**



