## 邀请码 /invitation

邀请码模块包含：邀请码校验、获取邀请码、返佣规则

---

#### **1.校验邀请码**

```
GET    http://localhost:8082/auth/invitation/code/check/{invitationCode}
```

* **参数说明：**
  * String **invitationCode : 6位唯一邀请码**
* **返回结果：**

```
SUCCESS    // 验证成功
NOT_EXISTS  // 验证码不存在
NONE       // 验证码次数用完
```

* **异常情况：无**

#### 2.获取邀请码

```
GET    http://localhost:8082/auth/invitation/code
```

* **返回结果：**

```
8aC2KE
```

* **异常情况：无**

#### 3.获取返佣规则

```
GET    http://localhost:8082/auth/invitation/level/description
```

* **接口使用说明：**
  * ruleMap：
    * 只显示生效的返佣规则。
    * 如果后台清退用户返佣，数据可能为空。
* **返回结果：**

```
{
  "id": 1,
  "nameCN": "铜牌",
  "nameEN": "Bronze Medal",
  "nameJP": "銅メダル",
  "nameKR": "동메달",
  "ruleMap": {
    "1": {
      "level": 1,
      "expire": 90,
      "referralRewardRate": 0,
      "expiredDate": "2019-05-13T16:53:45Z",
      "status": "ON"
    }
  }
}
```

* **异常情况：无**



