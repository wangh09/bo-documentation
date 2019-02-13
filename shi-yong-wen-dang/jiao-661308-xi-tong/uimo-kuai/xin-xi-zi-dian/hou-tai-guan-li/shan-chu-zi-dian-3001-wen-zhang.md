#### 1.删除某一字典列

```
DELETE    http://localhost:8082/ui/info/manage/delete/{dictId}
```

* **接口说明：超级管理员权限**

  * **该操作会自动删除文章内容表的相关项（如果没有不会删除，有一定删除）**

* 参数说明：

  * Long  ditcId :  主键

* 返回结果：

  * ```
    “OK”
    ```

#### 2.删除多列字典项

```
DELETE    http://localhost:8082/ui/info/manage/delete/batch
```

* **接口说明同上**
* 参数说明：
  * ```
    [100,101,102]
    ```
* 返回结果：

  * ```
    “OK”
    ```



