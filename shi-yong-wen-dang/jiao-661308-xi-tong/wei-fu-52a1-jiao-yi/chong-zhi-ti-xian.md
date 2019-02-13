## 充值提现功能  /finance

#### 1.获取指定币种充值规则

```
GET    http://47.92.88.235:8082/mapi/finance/deposit-currency-rules/{currency}
```

* 参数：{currency}币种（BTC、INK、ETH）
  * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常
* 返回结果：

  * ```
    {
      "title": "deposit-currency-rules",
      "status": 200,
      "data": {
        "rules": [
          {
            "amount": 2,
            "confirms": 12
          },
          {
            "amount": 0,
            "confirms": 1
          }
        ]
      },
      "timestamp": 1529588900366
    }
    ```

#### 2.获取指定币种充值记录

```
GET    http://47.92.88.235:8082/mapi/finance/deposit/logs
```

* 参数：{currency}币种（BTC、INK、ETH），startTime开始时间，endTime结束时间，pageSize几条数据，pageNum第几页
  * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常
* 返回结果：

  * ```
    {
    "title": "deposit logs",
    "status": 200,
    "data": [
    {
    "id": 2,
    "currency": "ETH",
    "toAddress": "0x94c7e9933e0c66cc9af78aaea0467d8bfc191997",
    "uniqueId": "0xd5d8530c087e6c6482f56baf61c7c30a6b103ceae4744e1878f5eaf944c13f17#0xd28def3a0861b60095e49e34f33b616183f424de56c2dac4e796370adfd5cd50",
    "amount": 0.1000000000000000,
    "confirms": 13,
    "minimumConfirms": 12,
    "depositOk": false,
    "depositCancelled": false,
    "createdAt": 1528440454281
    },
    {
    "id": 1,
    "currency": "INK",
    "toAddress": "0x94c7e9933e0c66cc9af78aaea0467d8bfc191997",
    "uniqueId": "0x774caefef61555564ab007fef8d392f3b63b2767161013cb45844867546300a2#0x87e4bcce14e23170dac31dee240e8e6a2dc7b59adb618b1a6ddc1acb3528b853",
    "amount": 80.0000000000000000,
    "confirms": 13,
    "minimumConfirms": 12,
    "depositOk": false,
    "depositCancelled": false,
    "createdAt": 1528274425655
    }
    ],
    "timestamp": 1529590128665,
    "pageSize": 5,
    "pageNum": 1,
    "pageTotal": 1
    }
    ```

#### 3.获取指定币种充值地址

```
GET    http://47.92.88.235:8082/mapi/finance/deposit/{currency}/address
```

* 参数：{currency}币种（BTC、INK、ETH）
  * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常
* 返回结果：

  * ```
    {
      "title": "deposit address",
      "status": 200,
      "data": {
        "id": 100003,
        "currency": "ETH",
        "address": "0x09a77c9235edff1e56439795f2be157c77c5cfee",
        "description": null,
        "createdAt": 1528424357664
      },
      "timestamp": 1529594187927
    }
    ```

#### 4.获取指定币种个人账户

```
GET    http://47.92.88.235:8082/mapi/finance/spot-account/{currency}
```

* 参数：{currency}币种（BTC、INK、ETH）
  * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常
* 返回结果：

  * ```
    {
      "title": "get mat-user spot-account",
      "status": 200,
      "data": {
        "spotAccounts": [
          {
            "currency": "INK",
            "type": "SPOT_AVAILABLE",
            "balance": 0.7,
            "id": 100325,
            "createdAt": 1528440632230,
            "updatedAt": 1528441691770,
            "version": 0,
            "userId": 100004,
            "withdrawflag": false,
            "depositflag": false,
            "tradeflag": false
          }
        ]
      },
      "timestamp": 1529594319468
    }
    ```

#### 5.添加充值地址

```
POST    http://47.92.88.235:8082/mapi/finance/withdraw/address
```

* 参数：
  * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常
  * ```
    {
      "address": "string",
      "currency": "string",
      "description": "string"
    }
    ```
* 返回结果：

  * ```
    {
      "title": "get mat-user spot-account",
      "status": 200,
      "data": {
        "spotAccounts": [
          {
            "currency": "INK",
            "type": "SPOT_AVAILABLE",
            "balance": 0.7,
            "id": 100325,
            "createdAt": 1528440632230,
            "updatedAt": 1528441691770,
            "version": 0,
            "userId": 100004,
            "withdrawflag": false,
            "depositflag": false,
            "tradeflag": false
          }
        ]
      },
      "timestamp": 1529594319468
    }
    ```

## 充值提现功能  /finance

#### 1.获取指定币种充值规则

```
GET    http://47.92.88.235:8082/mapi/finance/deposit-currency-rules/{currency}
```

* 参数：{currency}币种（BTC、INK、ETH）
  * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常
* 返回结果：

  * ```
    {
      "title": "deposit-currency-rules",
      "status": 200,
      "data": {
        "rules": [
          {
            "amount": 2,
            "confirms": 12
          },
          {
            "amount": 0,
            "confirms": 1
          }
        ]
      },
      "timestamp": 1529588900366
    }
    ```

#### 2.获取指定币种充值记录

```
GET    http://47.92.88.235:8082/mapi/finance/deposit/logs
```

* 参数：{currency}币种（BTC、INK、ETH），startTime开始时间，endTime结束时间，pageSize几条数据，pageNum第几页
  * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常
* 返回结果：

  * ```
    {
    "title": "deposit logs",
    "status": 200,
    "data": [
    {
    "id": 2,
    "currency": "ETH",
    "toAddress": "0x94c7e9933e0c66cc9af78aaea0467d8bfc191997",
    "uniqueId": "0xd5d8530c087e6c6482f56baf61c7c30a6b103ceae4744e1878f5eaf944c13f17#0xd28def3a0861b60095e49e34f33b616183f424de56c2dac4e796370adfd5cd50",
    "amount": 0.1000000000000000,
    "confirms": 13,
    "minimumConfirms": 12,
    "depositOk": false,
    "depositCancelled": false,
    "createdAt": 1528440454281
    },
    {
    "id": 1,
    "currency": "INK",
    "toAddress": "0x94c7e9933e0c66cc9af78aaea0467d8bfc191997",
    "uniqueId": "0x774caefef61555564ab007fef8d392f3b63b2767161013cb45844867546300a2#0x87e4bcce14e23170dac31dee240e8e6a2dc7b59adb618b1a6ddc1acb3528b853",
    "amount": 80.0000000000000000,
    "confirms": 13,
    "minimumConfirms": 12,
    "depositOk": false,
    "depositCancelled": false,
    "createdAt": 1528274425655
    }
    ],
    "timestamp": 1529590128665,
    "pageSize": 5,
    "pageNum": 1,
    "pageTotal": 1
    }
    ```

#### 3.获取指定币种充值地址

```
GET    http://47.92.88.235:8082/mapi/finance/deposit/{currency}/address
```

* 参数：{currency}币种（BTC、INK、ETH）
  * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常
* 返回结果：

  * ```
    {
      "title": "deposit address",
      "status": 200,
      "data": {
        "id": 100003,
        "currency": "ETH",
        "address": "0x09a77c9235edff1e56439795f2be157c77c5cfee",
        "description": null,
        "createdAt": 1528424357664
      },
      "timestamp": 1529594187927
    }
    ```

#### 4.获取指定币种个人账户

```
GET    http://47.92.88.235:8082/mapi/finance/spot-account/{currency}
```

* 参数：{currency}币种（BTC、INK、ETH）
  * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常
* 返回结果：

  * ```
    {
      "title": "get mat-user spot-account",
      "status": 200,
      "data": {
        "spotAccounts": [
          {
            "currency": "INK",
            "type": "SPOT_AVAILABLE",
            "balance": 0.7,
            "id": 100325,
            "createdAt": 1528440632230,
            "updatedAt": 1528441691770,
            "version": 0,
            "userId": 100004,
            "withdrawflag": false,
            "depositflag": false,
            "tradeflag": false
          }
        ]
      },
      "timestamp": 1529594319468
    }
    ```

#### 6.获取提现请求

```
GET    http://47.92.88.235:8082/mapi/finance/withdraw/requests
```

* 参数：{currency}币种（BTC、INK、ETH），startTime开始时间，endTime结束时间，pageSize几条数据，pageNum第几页

  * * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常

* 返回结果：

  * ```
    {
      "title": "withdraw requests",
      "status": 200,
      "data": [
        {
          "id": 3,
          "userId": 100003,
          "status": "CANCELLED",
          "errorCode": "",
          "errorMessage": "",
          "currency": "INK",
          "toAddress": "0x09a77c9235edff1e56439795f2be157c77c5cfee",
          "amount": 0.27,
          "fee": 0.01,
          "tx": "",
          "cancellable": false,
          "createdAt": 1528442516074,
          "updateAt": 0
        },
        {
          "id": 2,
          "userId": 100003,
          "status": "DONE",
          "errorCode": "",
          "errorMessage": "",
          "currency": "INK",
          "toAddress": "0x09a77c9235edff1e56439795f2be157c77c5cfee",
          "amount": 0.2,
          "fee": 0.01,
          "tx": "0x39f6f401f7adffedee8b37726c32b2290b1f7a7f5803bf6b94a839b09bb1985e",
          "cancellable": false,
          "createdAt": 1528438960252,
          "updateAt": 0
        },
        {
          "id": 1,
          "userId": 100003,
          "status": "DONE",
          "errorCode": "",
          "errorMessage": "",
          "currency": "INK",
          "toAddress": "0x09a77c9235edff1e56439795f2be157c77c5cfee",
          "amount": 0.5,
          "fee": 0.01,
          "tx": "0xce3b5fa28b973a9852eea0d5b9819c3d84f67f20055f809da6d8f51067b11b3b",
          "cancellable": false,
          "createdAt": 1528426597674,
          "updateAt": 0
        }
      ],
      "timestamp": 1529594799318,
      "pageSize": 5,
      "pageNum": 1,
      "pageTotal": 1
    }
    ```

#### 7.获取提现规则

```
GET    http://47.92.88.235:8082/mapi/finance/withdraw/rule/{currency}
```

* 参数：{currency}币种（BTC、INK、ETH）

  * * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常

* 返回结果：

  * ```
    {
      "title": "withdraw rule",
      "status": 200,
      "data": {
        "withdrawDisabled": false,
        "minimumAmount": 0.1,
        "feeRate": 0.0001,
        "minimumFee": 0.01,
        "maximumFee": 0.05
      },
      "timestamp": 1529594906674
    }
    ```

#### 8.获取提现地址

```
GET    http://47.92.88.235:8082/mapi/finance/withdraw/{currency}/address
```

* 参数：{currency}币种（BTC、INK、ETH）,pageSize几条数据，pageNum第几页

  * * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常

* 返回结果：

  * ```
    {
      "title": "withdraw addresses",
      "status": 200,
      "data": [
        {
          "id": 1,
          "userId": 100003,
          "currency": "INK",
          "address": "0x09a77c9235edff1e56439795f2be157c77c5cfee",
          "description": "100004",
          "createdAt": 1528425132912
        }
      ],
      "timestamp": 1529595119936,
      "pageSize": 5,
      "pageNum": 1,
      "pageTotal": 1
    }
    ```



