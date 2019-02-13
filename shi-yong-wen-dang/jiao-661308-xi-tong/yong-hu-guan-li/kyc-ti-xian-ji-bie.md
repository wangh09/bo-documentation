#### 1.新建、修改 KYC 提现

```
POST    http://localhost:8080/user/level/kyc/limits
```

* **参数说明：id 为 null 新建，有值则更新**

```
{
  "id": 1,
  "kycLevel": "C0",
  "withdrawLimit": 0
}
```

* **返回结果：**

```
{
  "id": 1,
  "kycLevel": "C0",
  "withdrawLimit": 0
}
```

* **异常情况：无**

#### **2.新建、修改 VIP 提现（暂未使用）**

```
POST    http://localhost:8080/user/level/vip/limits
```

* **参数说明：**

```
{
  "id": 0,
  "status": true,
  "userId": 5,
  "vipLevel": "string",
  "withdrawLimit": 0
}
```

* **返回结果：**

```
{
  "id": 0,
  "status": true,
  "userId": 0,
  "vipLevel": "string",
  "withdrawLimit": 0
}
```

* **异常情况：无**



