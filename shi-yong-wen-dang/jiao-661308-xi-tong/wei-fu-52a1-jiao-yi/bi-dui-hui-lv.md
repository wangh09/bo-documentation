币对汇率功能  /rate

#### 1.获取币对的汇率

```
GET    http://47.92.88.235:8082/mapi/rate/symbol
```

* 参数：baseSymbol：基准货币，quoteSymbol：计价货币

* 返回结果：

  * ```
    {
      "title": "get symbol rate",
      "status": 200,
      "data": {
        "id": 80317,
        "baseSymbol": "ETH",
        "quoteSymbol": "BTC",
        "rate": 0.0788044905,
        "coinId": 1027,
        "createTime": 1529488906118,
        "updateTime": 1529596435396
      },
      "timestamp": 1529596444352
    }
    ```

#### 2.法币对法币，法币对计价货币的转换

```
GET    http://47.92.88.235:8082/mapi/rate/symbol/currency
```

* 参数：baseSymbol：基准货币，quoteSymbol：计价货币

* 返回结果：

  * ```
    {
      "title": "get currency rate",
      "status": 200,
      "data": 3476.14467396,
      "timestamp": 1529596761215
    }
    ```



