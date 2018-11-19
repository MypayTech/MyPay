<p align="center">
<h3 align="center">MyPay —— 汇率接口</h3><hr>
</p>

```
这边提供的查询汇率接口，服务器1分钟更新一次，查询缓存显示整点数据。
```


#### 请求:

```
Method: HTTP GET

https://mypay.iemoney.co.nz/rate/query_rate
```

#### 返回:

```

 {
    "is_success": "TRUE",
    "message": "QUERY RATE",
    "extra": [
        {
            "id": "12",
            "type": "alipay",
            "currency": "NZD",
            "rate": "4.6536",
            "ct": "2018-04-16 11:00:01"
        },
        {
        "id": "12",
        "type": "alipay_online",
        "currency": "NZD",
        "rate": "4.6536",
        "ct": "2018-04-16 11:00:01"
        },
        {
            "id": "11",
            "type": "wechat",
            "currency": "NZD",
            "rate": "4.636",
            "ct": "2018-04-16 11:00:01"
        }
    ]
}
 
```


