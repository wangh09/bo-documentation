#### 1.发送站内信

```
POST    http://localhost:8080/web-server/message/send
```

* **接口说明：\[ \] 参数根据站内信类型选择**

  * **发送站内信 ：**
    * **全站：**
      * String **type : PUBLIC**
    * **分组：**
      * String **type : GROUP**
      * String **groupName :  站内信分组名称**
    * **私信：**
      * String **type ：PRIVATE**
      * String **receiverArray : "1;2;3"  【以 ;  分割接收用户 id】**

```
{
  ["groupName": "LEVEL1",]
  ["receiverArray": "4;5;10",]
  "senderId": "m-100001",
  "textList": [
    {
      "content": "站内信测试第一条",
      "isShow": true,
      "language": "zh-CN",
      "title": "站内信测试"
    },
   ....[en-US]、[ko-KR]、[ja-JP]
  ],
  "type": "PRIVATE"
}
```

* **返回结果：**

```
trur / false
```

* **异常情况：无**

---

#### 2.编辑已发送站内信内容（该功能暂时不使用）

```
POST    http://localhost:8080/web-server/message/edit
```

* **接口说明：如需更改类型、组名、接收用户，可以直接删除站内信内容，该信息不会保存在用户列表中（慎用）。**

  * **默认只允许修改信息内容，不允许修改：**

    * **type（信息类型）**

    * **receiverArray （接收用户）**

    * **groupName（分组名称）**

      * **参数补填**
        * **Long  msgId**
        * **Long id \[ 站内信内容 ID \]**
        * **String  msgTextId  \[ 同一内容的不同语种信息  拥有相同的 msgTextId \]**

* **参数说明：**

```
{
    "msgId": 108,
    "receiverArray": "12",
    "senderId": "m-01",
    "textList": [
        {
            "id":5,
            "msgTextId": "e99524d8e7ec441a976b38ee13820cbc",
            "title": "测试-修改",
            "content": "站内信测试内容-修改",
            "language": "zh-CN",
            "isShow": true
        },
        ......[en-US]、[ja-JP]、[ko-KR]
    ],
    "type": "PRIVATE"
}

```

* **返回结果：**

```
{
  "msgId": 108,
  "senderId": "m-01",
  "type": "PRIVATE",
  "receiverArray": "12",
  "groupName": null,
  "textList": [
    {
      "id": 209,
      "msgTextId": "e99524d8e7ec441a976b38ee13820cbc",
      "title": "测试-修改",
      "content": "站内信测试内容-修改",
      "language": "zh-CN",
      "isShow": true,
      "createdBy": "anonymousUser",
      "createdDate": "2018-08-13T15:17:23Z",
      "lastModifiedBy": "anonymousUser",
      "lastModifiedDate": "2018-08-13T15:17:23Z"
    },
    ......[en-US]、[ja-JP]、[ko-KR]
  ]
}
```

* **异常情况：**
  * **500  补填参数不完整 （UI 模块 400）**



