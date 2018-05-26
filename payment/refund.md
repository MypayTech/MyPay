<p align="center">
<h3 align="center">MyPay —— 退款接口</h3><hr>
</p>

```
这边提供的退款接口，只能当天退款，避免财务结算后的流程问题。隔T+1天（工作日），需要提交工单，手动退款。
目前只支持退款一次，支持部分金额退款。多次退款请联系开发人员。
通过平台退款的，没有手续费的成本，原路径返回。
```


#### 请求:

```
Method: HTTP POST

https://mypay.iemoney.co.nz/api/refund
```

|Parameter	|Type 	 |Description|
|-----------|--------|-----------|
|mid        |int     |5位数，这边获取注册|
|out_trade_no |int   |唯一订单号|
|pay_type   |string  |支付类型IE0011,IE0012,IE0013,IE0021,IE0022|
|refund_amount |int  |退款金额，单位：分|
|sign       |string  |签名，签名规则 sign md5(mid.out_trade_no.pay_type.refund_amount.api_key)<br/>api_key 通过平台注册时获取|

#### 返回:

```
 {
    "is_success": "TRUE",
    "message": "SUCCESS",
    "extra": []
 }
 
```


