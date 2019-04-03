#### **1. 创建返佣级别和规则**

```
POST    http://localhost:8080/invitation/level/rule
```

* **参数说明：**

```
{
  "level": {
    "id": 0,
    "nameCN": "string",
    "nameEN": "string",
    "nameJP": "string",
    "nameKR": "string",
    "createdBy": "string",
    "lastModifiedBy": "string"
  },
  "ruleList": [
    {
      "expire": 0,
      "id": 0,
      "level": 0,
      "levelId": 0,
      "levelStatus": "ON",
      "referralRewardRate": 0,
      "createdBy": "string",
      "lastModifiedBy": "string"
    }
  ]
}
```



