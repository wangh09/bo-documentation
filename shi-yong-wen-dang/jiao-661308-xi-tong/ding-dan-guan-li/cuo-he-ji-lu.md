#### 1.获取撮合记录首页统计

```
GET    http://localhost:8080/manager/match/list
```

* **接口说明：获取撮合记录首页统计**
* **参数说明：**

* **返回结果：**

```
[
  {
    "symbol": "USDT_BTC",
    "matchAmount": 26334.0001,
    "matchNumber": 27,
    "matchTotal": 41256.90008179,
    "createAt": 1546502464269
  },
  {
    "symbol": "ZEC_BTC",
    "matchAmount": 713.1,
    "matchNumber": 6,
    "matchTotal": 231.68515255,
    "createAt": 1546502464274
  }
]
```

* **异常情况：无**

#### 2.获取撮合记录统计详情

```
GET    http://localhost:8080/manager/match/page
```

* **接口说明：获取撮合记录统计详情**
* **参数说明：**

  * Long businessId : 业务层用户ID
  * String symbol : 币对
  * String type : 默认查询全部
  * BigDecimal priceLow : 低价
  * BigDecimal priceHigh : 高价
  * Integer page : 1
  * Integer size : 10
  * Long startTime : 开始时间\(可选\)
  * Long endTime : 结束时间\(可选\)

* **返回结果：**

```
{
  "pageNum": 1,
  "pageSize": 10,
  "size": 10,
  "orderBy": null,
  "startRow": 1,
  "endRow": 10,
  "total": 32,
  "pages": 4,
  "list": [
    {
      "id": 100069,
      "makerId": 100001,
      "makerBusinessId": 11114,
      "takerId": 100001,
      "takerBusinessId": 11114,
      "amount": 2,
      "price": 5,
      "takerFee": 0.05,
      "makerEmail": null,
      "takerEmail": null,
      "makerFee": 0.01,
      "createdAt": 1545910595270
    }
  ],
  "firstPage": 1,
  "prePage": 0,
  "nextPage": 2,
  "lastPage": 4,
  "isFirstPage": true,
  "isLastPage": false,
  "hasPreviousPage": false,
  "hasNextPage": true,
}
```

* **异常情况：400 币对无效**

#### 3.导出撮合记录统计详情

```
GET    http://localhost:8080/manager/match/export/csv
```

* **接口说明：导出撮合记录统计详情**
* **参数说明：**

  * Long businessId : 业务层用户ID
  * String symbol : 币对
  * String type : 默认查询全部
  * BigDecimal priceLow : 低价
  * BigDecimal priceHigh : 高价
  * Integer page : 1
  * Integer size : 10
  * Long startTime : 开始时间\(可选\)
  * Long endTime : 结束时间\(可选\)

* **返回结果：**

```

```

* **异常情况：400 币对无效**



