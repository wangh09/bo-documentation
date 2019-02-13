#### 1.获取盘口查询首页统计

```
GET    http://localhost:8080/manager/handicap/list
```

* **接口说明：获取盘口查询首页统计**
* **参数说明：**

* **返回结果：**

```
[
  {
    "symbol": "USDT_BTC",
    "buyNumber": null,
    "buyAmount": 59684.7834,
    "buyDealAmount": 26334.0001,
    "buyTotal": 41292.62453282992,
    "buyDealTotal": 41256.90008179,
    "sellNumber": null,
    "sellAmount": 30178,
    "sellDealAmount": 26334.0001,
    "sellTotal": 3019.60007179,
    "sellDealTotal": 41256.90008179,
    "createAt": 1546504264298
  },
  {
    "symbol": "ZEC_BTC",
    "buyNumber": null,
    "buyAmount": 713.1,
    "buyDealAmount": 713.1,
    "buyTotal": 1830.59381631,
    "buyDealTotal": 231.68515255,
    "sellNumber": null,
    "sellAmount": 713.1,
    "sellDealAmount": 713.1,
    "sellTotal": 231.68515255,
    "sellDealTotal": 231.68515255,
    "createAt": 1546504264302
  }
]
```

* **异常情况：无**

#### 2.获取盘口查询统计详情

```
GET    http://localhost:8080/manager/handicap/page
```

* **接口说明：获取盘口查询统计详情**
* **参数说明：**

  * Long businessId : 业务层用户ID
  * String symbol : 币对
  * String type : ALL \(默认查询全部\)
  * String status : 订单状态（ALL,SEQUENCED,PARTIAL\_FILLED）

  * Integer page : 1

  * Integer size : 10
  * Long startTime : 开始时间\(可选\)
  * Long endTime : 结束时间\(可选\)

* **返回结果：**

```
{
  "pageNum": 1,
  "pageSize": 10,
  "size": 2,
  "orderBy": null,
  "startRow": 1,
  "endRow": 2,
  "total": 2,
  "pages": 1,
  "list": [
    {
      "id": 100176,
      "createdAt": 1546419970500,
      "updatedAt": 0,
      "seqId": 0,
      "refOrderId": 0,
      "refSeqId": 0,
      "userId": 100001,
      "source": null,
      "symbol": "ETH_BTC",
      "mining": null,
      "type": "SELL_LIMIT",
      "price": 5,
      "amount": 2,
      "filledAmount": 0,
      "fee": null,
      "triggerOn": null,
      "features": 0,
      "status": "SEQUENCED",
      "averagePrice": null,
      "businessId": 11114,
      "email": null
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

* **异常情况：400 币对无效**



