#### 1.获取手动转账操作日志

```
GET    http://localhost:8080/asset/flows/manual
```

* **接口说明：**获取手动转账操作日志
* **参数说明：**

  * Integer page : 0
  * Integer size : 10
  * Long startTime : 开始时间\(可选\)
  * Long endTime : 结束时间\(可选\)

* **返回结果：**

```
{
  "content": [
    {
      "id": 101,
      "operatorId": 5,
      "operator": "zhouhong",
      "ipAddress": "61.50.105.122",
      "fromUserId": 103,
      "fromUserType": "ASSET",
      "toUserId": 106,
      "toUserType": "WITHDRAW_FEE",
      "currency": "TOC",
      "amount": 1,
      "operationType": "TRANSFER",
      "withdrawUserId": null,
      "remarks": "현찰現像カード",
      "createTime": 1545819900259
    }
  ],
  "pageable": {
    "sort": {
      "unsorted": true,
      "sorted": false
    },
    "pageSize": 20,
    "pageNumber": 0,
    "offset": 0,
    "paged": true,
    "unpaged": false
  },
  "last": false,
  "totalPages": 4,
  "totalElements": 78,
  "first": true,
  "sort": {
    "unsorted": true,
    "sorted": false
  },
  "numberOfElements": 20,
  "size": 20,
  "number": 0
}
```

* **异常情况：无**





#### 2.获取自动转账操作日志

```
GET    http://localhost:8080/asset/flows/automatic
```

* **接口说明：**获取自动转账操作日志
* **参数说明：**

  * Integer page : 0
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
  "total": 134,
  "pages": 14,
  "list": [
    {
      "id": 100837,
      "createdAt": 1546160400285,
      "flowType": "WITHDRAW_ASSET",
      "fromUserId": 106,
      "fromAccountId": 0,
      "toUserId": 103,
      "toAccountId": 0,
      "currency": "ETH",
      "amount": 0.02998623104835,
      "description": "2018-12-30 17:00:00 Asia/Shanghai:ETH:0.029986231048350000"
    }
  ],
  "firstPage": 1,
  "prePage": 0,
  "nextPage": 2,
  "lastPage": 8,
  "isFirstPage": true,
  "isLastPage": false,
  "hasPreviousPage": false,
  "hasNextPage": true,
}
```

* **异常情况：无**



