## 工单系统

#### 1.提交工单

```
POST    http://47.92.88.235:8082/info/work-request
```

* 参数：
  * ```
    { 
      "reqNum":,         // 工单号 
      "userId": ,        // 用户 id
      "userLevel": ,     // 用户级别
      "userMobile":"",   // 用户电话 （可以发送短信通知工单情况，提高用户体验）
      "userContact":"",  // 联系方式
      "serverId": ,      // 工作人员 id
      "satisfaction":,   // 用户对工单的满意度
      "reqType":"",      // 工单类型
      "reqTitle":"",     // 工单标题
      "replayStatus":"", // 回复状态
      "replayText":"",   // 回复内容
      "sequence":
    }
    ```

#### 2.提交工单照片

```
POST    http://47.92.88.235:8082/info/work-request/img
```

* 参数：

#### 3.查看工单列表

```
GET    http://47.92.88.235:8082/info/work-request
```

* 返回结果：

  * ```

    ```

#### 4.取消工单

```
GET    http://47.92.88.235:8082/info/work-request/cancel/{reapairId}
```

* 参数：Long **reapairId**
* 返回结果：

  * ```

    ```



