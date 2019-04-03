#### **1. 创建返佣级别和规则**

```
POST    http://localhost:8080/invitation/level/rule
```

* **接口使用说明：\[ \] 参数为更新必传，更新不传 createdBy 字段。**
  * **创建、更新奖牌：** level 数据。
  * **创建、更新奖牌规则：** ruleList （ levelId 创建、更新必传）数据。
  * **创建奖牌和奖牌规则：**lelvel、ruleList （如果创建 levelId 不传）数据。
* **参数说明：**

```
{
  "level": {
    ["id": 2,]
    "nameCN": "银牌",
    "nameEN": "Silver Medal",
    "nameJP": "銀メダル",
    "nameKR": "은메달",
    "createdBy": "bonismo"
    ["lastModifiedBy": "bonismo"]
  },
  "ruleList": [
    {
      ["id": 2,]
      ["levelId": 2,]
      "expire": 90,
      "level": 1,
      "levelStatus": "ON",
      "referralRewardRate": 0.2,
      "createdBy": "boinismo"
      ["lastModifiedBy": "bonismo"]
    }
  ]
}
```

* **返回结果：**

```
{
  "level": {
    "id": 2,
    "nameCN": "银牌",
    "nameEN": "Silver Medal",
    "nameJP": "銀メダル",
    "nameKR": "은메달",
    "extension": null,
    "description": null,
    "createdBy": "bonismo",
    "createdDate": "2019-04-03T06:00:46.472Z",
    "lastModifiedBy": "bonismo",
    "lastModifiedDate": "2019-04-03T06:00:46.472Z"
  },
  "ruleList": [
    {
      "id": 2,
      "levelId": 2,
      "level": 1,
      "expire": 90,
      "referralRewardRate": 0.2,
      "levelStatus": "ON",
      "extension": null,
      "description": null,
      "createdBy": "boinismo",
      "createdDate": "2019-04-03T06:00:46.485Z",
      "lastModifiedBy": "boinismo",
      "lastModifiedDate": "2019-04-03T06:00:46.485Z"
    }
  ]
}
```

* **异常情况：无**

#### 2.分页获取返佣规则

```
GET    http://localhost:8080/invitaion/level/rule?page={page}&size={size}&sort={id,desc}
```

* **参数说明：**参考分页参数

* **返回结果：**

```
{
  "content": [
    {
      "level": {
        "id": 1,
        "nameCN": "铜牌",
        "nameEN": "Bronze Medal",
        "nameJP": "銅メダル",
        "nameKR": "동메달",
        "extension": "",
        "createdBy": "admin",
        "createdDate": "2019-04-01T03:38:56Z",
        "lastModifiedBy": "admin",
        "lastModifiedDate": null
      },
      "ruleList": [
        {
          "id": 1,
          "levelId": 1,
          "level": 1,
          "expire": 90,
          "referralRewardRate": 0,
          "levelStatus": "ON",
          "extension": "",
          "description": "",
          "createdBy": "admin",
          "createdDate": "2019-04-01T03:38:57Z",
          "lastModifiedBy": "admin",
          "lastModifiedDate": null
        },
        ...... [other data]
      ]
    },
    ...... [other data]
  ],
  "last": true,
  "totalElements": 10,
  "totalPages": 1,
  "size": 10,
  "number": 0,
  "sort": [
    {
      "direction": "ASC",
      "property": "id",
      "ignoreCase": false,
      "nullHandling": "NATIVE",
      "ascending": true,
      "descending": false
    }
  ],
  "first": true,
  "numberOfElements": 3
}
```

* **异常情况：无**

#### 3.获取用户邀请基本信息

```
GET    http://localhost:8080/invitation/basic/{userId}
```

* **请求参数：**
  * String userId 
* ** 返回参数说明：**

  * **ruleMap：**奖牌规则及其对应的数据

    * **level：**代表规则级别，和该数据的 key 一致

    * **expire：**有效天数

    * **expriedDate：**有效日期 （expiredDate - expire = 用户的 createdDate）

    * **referralRewardRate：**返佣比例

    * **status：**规则状态（ON 开启 / DOWN 关闭）

  * **levelCountMap：**规则内邀请用户数量

  * **referrlaRewardMap：**佣金数据（此处不展示，null）

* **返回结果：**

```
{
  "userId": 11198,
  "email": "bonismo@qq.com",
  "invitationCode": "P5Xa56",
  "ruleVM": {
    "id": 1,
    "nameCN": "铜牌",
    "nameEN": "Bronze Medal",
    "nameJP": "銅メダル",
    "nameKR": "동메달",
    "ruleMap": {
      "1": {
        "level": 1,
        "expire": 90,
        "referralRewardRate": 0.1,
        "expiredDate": "2019-07-02T07:33:36.832Z",
        "status": "ON"
      },
      "2": {
        "level": 2,
        "expire": 120,
        "referralRewardRate": 0.2,
        "expiredDate": "2019-08-01T07:33:36.832Z",
        "status": "ON"
      },
      "3": {
        "level": 3,
        "expire": 180,
        "referralRewardRate": 0.4,
        "expiredDate": "2019-09-30T07:33:36.832Z",
        "status": "ON"
      }
    }
  },
  "levelCountMap": {
    "1": 4,
    "2": 3,
    "3": 2
  },
  "referralRewardMap": null
}
```

* **异常情况：无**

#### 4.调整用户返佣规则

```
PUT    http://localhost:8082/auth/user/invitation/user/setting
```

* **接口使用说明：**
  * 根据用户邀请的基本信息（接口3）获取用户所有规则的返佣截止日期，未过期，调用该接口。已过期，不允许调用。
* **参数说明：**
  * Long **userId：用户 id**
  * String **medalType： **
    * **ADJUSTMENT 调级**
    * **CLEAR 清退（用户返佣状态关闭，底层不再返佣）**
    * **RESTORE 恢复（用户返佣状态开启，底层开始返佣）**
  * Long** levelId：调级时，使用 levelId（根据接口分页获取 level 的 id）。**
  * String **lastModifiedBy：操作人员**

```
{
  "userId": 11198,
  ["levelId": 1,]
  "medalType": "CLEAR",
  "lastModifiedBy": "bonismo",
}
```

* **返回结果：**

```
{
  "id": 10,
  "userId": 11198,
  "levelId": 1,
  "invitationCode": "P5Xa56",
  "invitationType": "REFERRAL_REWARD",
  "usedCount": -1,
  "basicUserId": 11198,
  "extension": "{\"id\":1,\"nameCN\":\"铜牌\",\"nameEN\":\"Bronze Medal\",\"nameJP\":\"銅メダル\",\"nameKR\":\"동메달\",\"ruleMap\":{1:{\"expire\":90,\"expiredDate\":\"2019-07-02T07:33:37Z\",\"level\":1,\"referralRewardRate\":0.1,\"status\":\"DOWN\"},2:{\"expire\":120,\"expiredDate\":\"2019-08-01T07:33:37Z\",\"level\":2,\"referralRewardRate\":0.2,\"status\":\"DOWN\"},3:{\"expire\":180,\"expiredDate\":\"2019-09-30T07:33:37Z\",\"level\":3,\"referralRewardRate\":0.4,\"status\":\"DOWN\"}}}",
  "description": null,
  "createdBy": "system",
  "createdDate": "2019-04-03T07:33:38Z",
  "lastModifiedBy": "bonismo",
  "lastModifiedDate": "2019-04-03T09:34:43Z"
}
```

* **异常情况：无**

#### 5.相关邀请信息综合查询

```
GET    http://localhost:8082/invitaiton/selector/{type}
```

* **接口使用说明：**
  * 查询所有用户邀请相关信息
  * 查询指定用户的下级相关信息
* **参数说明：**
  * String **type：**
    * **all 查询所有用户**
    * **single 查询指定用户**
  * Long **userId：用户 id**
  * String **email：邮箱**
    * **可支持模糊查询，通过开关开启**
    * **type = all 时，根据 email 查找相关用户**
    * **type = single 时，根据当前 userId 查询符合 email 相关用户**
  * Long **lowerUserId：**
    * **下级用户 id \(仅 type = single 时使用，根据当前 userId 查询 lowerUserId 信息\)**
  * Long **startDate：仅支持 type = single**
  * Long **endDate：仅支持 type = single**
  * **分页数据（支持 type = all、type = single）**
    * int page
    * int size
    * String sort
* **返回参数说明：返回结果已注释**
* **返回结果：**

```
{
  "content": [
    {
      "userId": 11214,
      "email": "napoleon@qq.com",
      "invitationCode": "P5TaV8",
      "relation": 1,                                  // 根节点距离
      "ruleVM": {
        "id": 1,
        "nameCN": "铜牌",
        "nameEN": "Bronze Medal",
        "nameJP": "銅メダル",
        "nameKR": "동메달",
        "ruleMap": {
          "1": {
            "level": 1,                                 // 返佣规则等级
            "expire": 90,                               // 返佣有效天数
            "referralRewardRate": 0.1,                  // 返佣比例
            "expiredDate": "2019-07-02T11:27:31.990Z",  // 返佣截止时间
            "status": "ON"                              // 返佣开启状态 ON / DOWN
          },
          "2": {
            "level": 2,
            "expire": 120,
            "referralRewardRate": 0.2,
            "expiredDate": "2019-08-01T11:27:31.990Z",
            "status": "ON"
          },
          "3": {
            "level": 3,
            "expire": 180,
            "referralRewardRate": 0.4,
            "expiredDate": "2019-09-30T11:27:31.990Z",
            "status": "ON"
          }
        }
      },
      "upperUserId": 11213,  // 上级 userId
      "lowerLevel": null,    // 该字段可以根据上次请求用户的 relation 返回 lowerLevel 显示该用户与上次用户的级别关系，暂不适用
      "levelCountMap": {     // 每级邀请的用户数量（根据该用户开启的返佣规则确定）
        "1": 0,
        "2": 0,
        "3": 0
      },
      "totalReferralReward": null,  // 返佣总额，该数据为 null，统一请求资金接口回去
      "createdDate": "2019-04-03T11:27:32Z" // 用户注册时间
    },
    ...... [other data]
],
  "number": 0,
  "size": 10,
  "totalElements": 10,
  "pageable": {
    "sort": {
      "sorted": false,
      "unsorted": true
    },
    "pageSize": 10,
    "pageNumber": 0,
    "offset": 0,
    "paged": true,
    "unpaged": false
  },
  "last": true,
  "totalPages": 1,
  "sort": {
    "sorted": false,
    "unsorted": true
  },
  "first": true,
  "numberOfElements": 10
}
```

* **异常情况：无**



