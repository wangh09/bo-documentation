## 通用配置功能  /common

#### 1.获取系统所有币种

```
GET    http://47.92.88.235:8082/mapi/common/currency
```

* 返回结果：

  * ```
    {
      "title": "Get all the currency",
      "status": 200,
      "data": {
        "currencies": [
          {
            "name": "BCH",
            "description": "Bitcoin Cash",
            "auditDeposit": false,
            "virtual": true
          },
          {
            "name": "BTC",
            "description": "Bitcoin",
            "auditDeposit": false,
            "virtual": true
          },
          {
            "name": "ETC",
            "description": "Ethereum Classic",
            "auditDeposit": false,
            "virtual": true
          },
          {
            "name": "ETH",
            "description": "Ethereum",
            "auditDeposit": false,
            "virtual": true
          },
          {
            "name": "INK",
            "description": "Ink",
            "auditDeposit": false,
            "virtual": true
          },
          {
            "name": "LTC",
            "description": "Litecoin",
            "auditDeposit": false,
            "virtual": true
          },
          {
            "name": "QTUM",
            "description": "Qtum",
            "auditDeposit": false,
            "virtual": true
          },
          {
            "name": "USD",
            "description": "US Dollar",
            "auditDeposit": false,
            "virtual": true
          }
        ]
      },
        "timestamp": 1529595966436
    }
    ```

#### 2.获取系统指定币种

```
GET    http://47.92.88.235:8082/mapi/common/currency/{currency}
```

* 参数：{currency}币种（BTC，ETH）

* 返回结果：

  * ```
    {
      "title": "Get someone currency",
      "status": 200,
      "data": {
        "name": "INK",
        "description": "Ink",
        "auditDeposit": false,
        "virtual": true
      },
      "timestamp": 1529596105046
    }
    ```

#### 3.获取系统所有币对

```
GET    http://47.92.88.235:8082/mapi/common/symbol
```

* 参数：

* 返回结果：

  * ```
    {
      "title": "Get all symbol",
      "status": 200,
      "data": {
        "symbols": [
          {
            "base": {
              "name": "BTC",
              "description": "Bitcoin",
              "auditDeposit": false,
              "virtual": true
            },
            "baseScale": 4,
            "baseMinimum": 0.0001,
            "quote": {
              "name": "USD",
              "description": "US Dollar",
              "auditDeposit": false,
              "virtual": true
            },
            "quoteScale": 2,
            "quoteMinimum": 1,
            "startTime": 0,
            "endTime": 9223372036854776000,
            "name": "BTC_USD",
            "quoteName": "USD",
            "baseName": "BTC"
          },
          {
            "base": {
              "name": "ETH",
              "description": "Ethereum",
              "auditDeposit": false,
              "virtual": true
            },
            "baseScale": 4,
            "baseMinimum": 0.0001,
            "quote": {
              "name": "BTC",
              "description": "Bitcoin",
              "auditDeposit": false,
              "virtual": true
            },
            "quoteScale": 4,
            "quoteMinimum": 0.0001,
            "startTime": 0,
            "endTime": 9223372036854776000,
            "name": "ETH_BTC",
            "quoteName": "BTC",
            "baseName": "ETH"
          },
          {
            "base": {
              "name": "ETH",
              "description": "Ethereum",
              "auditDeposit": false,
              "virtual": true
            },
            "baseScale": 4,
            "baseMinimum": 0.0001,
            "quote": {
              "name": "USD",
              "description": "US Dollar",
              "auditDeposit": false,
              "virtual": true
            },
            "quoteScale": 2,
            "quoteMinimum": 0.01,
            "startTime": 0,
            "endTime": 9223372036854776000,
            "name": "ETH_USD",
            "quoteName": "USD",
            "baseName": "ETH"
          },
          {
            "base": {
              "name": "INK",
              "description": "Ink",
              "auditDeposit": false,
              "virtual": true
            },
            "baseScale": 4,
            "baseMinimum": 0.0001,
            "quote": {
              "name": "ETH",
              "description": "Ethereum",
              "auditDeposit": false,
              "virtual": true
            },
            "quoteScale": 8,
            "quoteMinimum": 0.0001,
            "startTime": 1527480000000,
            "endTime": 1609430400000,
            "name": "INK_ETH",
            "quoteName": "ETH",
            "baseName": "INK"
          },
          {
            "base": {
              "name": "LTC",
              "description": "Litecoin",
              "auditDeposit": false,
              "virtual": true
            },
            "baseScale": 4,
            "baseMinimum": 0.0001,
            "quote": {
              "name": "USD",
              "description": "US Dollar",
              "auditDeposit": false,
              "virtual": true
            },
            "quoteScale": 2,
            "quoteMinimum": 0.01,
            "startTime": 0,
            "endTime": 9223372036854776000,
            "name": "LTC_USD",
            "quoteName": "USD",
            "baseName": "LTC"
          }
        ]
      },
      "timestamp": 1529596165789
    }
    ```

#### 4.获取系统指定币对

```
GET    http://47.92.88.235:8082/mapi/common/symbol/{symbol}
```

* 参数：

* 返回结果：

  * ```
    {
      "title": "Get someone symbol",
      "status": 200,
      "data": {
        "base": {
          "name": "BTC",
          "description": "Bitcoin",
          "auditDeposit": false,
          "virtual": true
        },
        "baseScale": 4,
        "baseMinimum": 0.0001,
        "quote": {
          "name": "USD",
          "description": "US Dollar",
          "auditDeposit": false,
          "virtual": true
        },
        "quoteScale": 2,
        "quoteMinimum": 1,
        "startTime": 0,
        "endTime": 9223372036854776000,
        "name": "BTC_USD",
        "quoteName": "USD",
        "baseName": "BTC"
      },
      "timestamp": 1529596260874
    }
    ```



