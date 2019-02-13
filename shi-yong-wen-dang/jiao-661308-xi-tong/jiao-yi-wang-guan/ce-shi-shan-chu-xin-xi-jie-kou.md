## 测试删除相关信息

#### 1.删除用户 Redis 信息

```
http://47.92.88.235:8082/auth/user/delete/user-redis/{email}
```

* **接口说明：**
  * **人为修改数据库，导致数据的不一致性。**
* **参数：**
  * String ** email**
* 返回结果：
  * ```
    账号存在：
    Response Code    200
    账号不存在：
    Response Code    400
    ```

#### 2.删除用户站内信

```
http://47.92.88.235:8082/ui/manager/delete-message-by/{userId}
```

* **接口说明：**
  * **删除用户的所有站内信（不包括私信 PRIVATE）**
* 返回结果：
  * ```
    账号存在：
    Response Code    200
    账号不存在：
    Response Code    400
    ```

#### 3.删除账号

```
http://localhost:8082/auth/user/delete/user/{email}
```

* **接口说明：**
  * **三个接口必须按照顺序操作，不然会有脏数据**
* 返回结果：
  * ```
    账号存在：
    Response Code    200
    账号不存在：
    Response Code    400
    ```



