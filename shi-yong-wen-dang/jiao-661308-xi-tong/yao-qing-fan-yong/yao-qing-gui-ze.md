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

#### 3.获取用户邀请详情

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



