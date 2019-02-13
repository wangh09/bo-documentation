#### 1.获取指定币种充值地址

```
GET    http://localhost:8080/asset/deposit/address/{currency}
```

* **接口说明：获取指定币种充值地址**
* **参数说明：**

  * String currency : 币种

* **返回结果：**

```
{
  "id": 100017,
  "currency": "ETH",
  "address": "0xeaddf1e0cbc09091a179b5674e1e7c7b8a0eda3e",
  "description": null,
  "createdAt": 1545220689823
}
```

* **异常情况：400 币种无效**

#### 2.获取指定币种充值记录

```
GET    http://localhost:8080/asset/deposit/log/{currency}
```

* **接口说明：获取指定币种充值记录**
* **参数说明：**

  * String currency : 币种
  * Integer page : 1
  * Integer size : 10
  * Long startTime : 开始时间\(可选\)
  * Long endTime : 结束时间\(可选\)

* **返回结果：**

```
{
  "pageNum": 1,
  "pageSize": 10,
  "size": 5,
  "orderBy": null,
  "startRow": 1,
  "endRow": 5,
  "total": 5,
  "pages": 1,
  "list": [
    {
      "id": 100017,
      "createdAt": 1545734548423,
      "updatedAt": 1545734669410,
      "status": "DEPOSITED",
      "userId": 108,
      "currency": "ETH",
      "uniqueId": "0xf991c508c3f94a337632ed4934ec8bd0343ed475eaff57a94236ebeb74c60f3f#0xe28644ab8a7d2574451e94e5cf323b5ae0ba74027824affc04d8b772065047eb",
      "amount": 18.75,
      "shouldAudit": false,
      "confirms": 10,
      "minimumConfirms": 10,
      "businessId": null,
      "initialaddress": "0xeaddf1e0cbc09091a179b5674e1e7c7b8a0eda3e"
    }
  ],
  "firstPage": 1,
  "prePage": 0,
  "nextPage": 0,
  "lastPage": 1,
  "isFirstPage": true,
  "isLastPage": true,
  "hasPreviousPage": false,
  "hasNextPage": false
}
```

* **异常情况：无**

#### 

#### 3.获取提现地址

```
GET    http://localhost:8080/asset/withdraw/address
```

* **接口说明：获取提现地址**
* **参数说明：**

* **返回结果：**

```
[
  {
    "id": 100008,
    "createdAt": 1545732502538,
    "userId": 108,
    "currency": "ETH",
    "addressHash": "b92e0d261ad859a354c95cca59471e687ee9e0516fd44475b070295b7c966b54",
    "encryptedAddress": "AES:000000000000006cc827aad76e965001c29788f775a6f9b739a58439e846ff88e292aa8e2ea050750930a9812637ad12bebe00385c8c49b82f21141b075604655d6cda2b98818259",
    "description": "sgy",
    "initialaddress": "0x3cfbd6fc9b92dafd27bbc07e6f660e19d78dfe7b",
    "toAddress": "0x3cfbd6fc9b92dafd27bbc07e6f660e19d78dfe7b"
  },
  {
    "id": 100009,
    "createdAt": 1545892853595,
    "userId": 108,
    "currency": "ETH",
    "addressHash": "3b1aaa6f24669f79d4b2440d3aa123b84da6efdf3c175664158c0943d94d4a74",
    "encryptedAddress": "AES:000000000000006cc827aad76e965001c29788f775a6f9b739a58439e846ff88e292aa8e2ea0507549f2f0f2988934a824a86808f35b48ef7e7cf0b380cc9e7af4d9d2633add5d95",
    "description": "123",
    "initialaddress": "0x3cfbd6fc9b92dafd27bbc07e6f660e19d78dfe7a",
    "toAddress": "0x3cfbd6fc9b92dafd27bbc07e6f660e19d78dfe7a"
  },
  {
    "id": 100012,
    "createdAt": 1546066313566,
    "userId": 108,
    "currency": "ETH",
    "addressHash": "cd5fbf15cc5bafd65d6c156d97a43680b44958fd591f2dbc5f917d18f83d3787",
    "encryptedAddress": "AES:000000000000006ce4bd5a31104b9cc8096b8e4ddeeff929eaac250e80d3e7dddbd883022d1ca7afb511994932d4e826defaafd7e53f76c0b04d60e4385bea0f415bea92ace14545",
    "description": "huan",
    "initialaddress": "0x2935e3a25ef6c402d099be95e4c770602f330c5d",
    "toAddress": "0x2935e3a25ef6c402d099be95e4c770602f330c5d"
  }
  .....
]
```

* **异常情况：无**

#### 4.添加提现地址

```
POST    http://localhost:8080/asset/withdraw/address
```

* **接口说明：添加提现地址**
* **参数说明：**

  ```
  {
    "address": "0xeaddf1e0cbc09091a179b5674e1e7c7b8a0eda3e",
    "currency": "ETH",
    "description": "ETH Address"
  }
  ```

* **返回结果：**

```
{
  "id": 100016,
  "userId": 108,
  "currency": "ETH",
  "address": "0xeaddf1e0cbc09091a179b5674e1e7c7b8a0eda3e",
  "description": "ETH Address",
  "createdAt": 1546497086781
}
```

* **异常情况：400 币种无效  地址已经存在**

#### 5.删除提现地址

```
DELETE    http://localhost:8080/asset/withdraw/{addressId}
```

* **接口说明：删除提现地址**
* **参数说明：**

  * Long addressId : 地址ID

* **返回结果：**

```
Boolean.TRUE
```

* **异常情况：无**

#### 6.创建提现请求

```
POST    http://localhost:8080/asset/withdraw/requests
```

* **接口说明：添加提现请求**
* **参数说明：**

  ```
  {
    "amount": "10",
    "currency": "ETH",
    "withdrawAddressId": 100000
  }
  ```

* **返回结果：**

```
{
  "id": 100038,
  "userId": 108,
  "status": "SUBMITTED",
  "errorCode": "",
  "errorMessage": "",
  "currency": "ETH",
  "toAddress": "0x2935e3a25ef6c402d099be95e4c770602f330c5d",
  "amount": 0.1,
  "fee": 0.011,
  "withdrawFee": 0.011,
  "tx": "",
  "cancellable": true,
  "createdAt": 1546497633173,
  "updateAt": 0
}
```

* **异常情况：400 币种无效  地址无效 数量不合法**

#### 7.获取指定币种提现规则

```
GET    http://localhost:8080/asset/withdraw/rule/{currency}
```

* **接口说明：获取指定币种提现规则**
* **参数说明：**

  * String currency : 币种

* **返回结果：**

```
{
  "id": 100013,
  "createdAt": 1545896266366,
  "updatedAt": 0,
  "version": 0,
  "withdrawDisabled": false,
  "minimumAmount": 0.01,
  "feeRate": 0.01,
  "feeOffset": 0.01,
  "minimumFee": 0.01,
  "maximumFee": 2,
  "currency": "ETH"
}
```

* **异常情况：400 币种无效**

#### 8.获取指定币种提现记录

```
GET    http://localhost:8080/asset/withdraw/log/{currency}
```

* **接口说明：获取指定币种提现记录**
* **参数说明：**

  * String currency : 币种
  * Integer page : 1
  * Integer size : 10
  * Long startTime : 开始时间\(可选\)
  * Long endTime : 结束时间\(可选\)

* **返回结果：**

```
{
{
  "pageNum": 1,
  "pageSize": 10,
  "size": 10,
  "orderBy": null,
  "startRow": 1,
  "endRow": 10,
  "total": 29,
  "pages": 3,
  "list": [
    {
      "id": 100038,
      "createdAt": 1546497633173,
      "updatedAt": 1546497664028,
      "status": "WAITING_FOR_APPROVAL",
      "errorCode": "",
      "errorMessage": "",
      "currency": "ETH",
      "userId": 108,
      "spotFrozenAccountId": 0,
      "encryptedToAddress": "AES:000000000000006ce4bd5a31104b9cc8096b8e4ddeeff929eaac250e80d3e7dddbd883022d1ca7afb511994932d4e826defaafd7e53f76c0b04d60e4385bea0f415bea92ace14545",
      "amount": 0.1,
      "tx": "",
      "withdrawFee": 0.011,
      "businessId": null,
      "initialaddress": "0x2935e3a25ef6c402d099be95e4c770602f330c5d",
      "toAddress": "0x2935e3a25ef6c402d099be95e4c770602f330c5d"
    }
  ],
  "firstPage": 1,
  "prePage": 0,
  "nextPage": 2,
  "lastPage": 3,
  "isFirstPage": true,
  "isLastPage": false,
  "hasPreviousPage": false,
  "hasNextPage": true
}
```

* **异常情况：400 币种无效**

#### 9.获取冷钱包用户详情

```
GET    http://localhost:8080/asset/cold-wallet/user
```

* **接口说明：获取冷钱包用户详情**
* **参数说明：**

* **返回结果：**

```
{
  "cold-wallet": {
    "id": 108,
    "createdAt": 1543991766276,
    "updatedAt": 1543991766276,
    "version": 0,
    "referrerId": 0,
    "organizationId": 0,
    "type": "COLD_WALLET",
    "level": 0,
    "internal": true,
    "canSignin": false,
    "canTrade": false,
    "canWithdraw": true
  },
  "asset": {
    "id": 103,
    "createdAt": 1543991766276,
    "updatedAt": 1543991766276,
    "version": 0,
    "referrerId": 0,
    "organizationId": 0,
    "type": "ASSET",
    "level": 0,
    "internal": true,
    "canSignin": false,
    "canTrade": false,
    "canWithdraw": false
  }
}
```

* **异常情况：无**



