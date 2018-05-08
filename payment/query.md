<p align="center">
<h3 align="center">MyPay —— 统一查询接口</h3><hr>
</p>

```
通过传递订单号和商户id查询订单状态
```


#### 请求:

```
Method: HTTP GET

https://mypay.iemoney.co.nz/api/check_order_status
```

|Parameter	|Type 	 |Description|
|-----------|--------|-----------|
|mid        |int     |5位数，这边获取注册|
|out\_trade_no   |string  |商户自己的订单号，32位，官方建议：时间日期，加随机数，唯一订单号|
|pay_type       |string     |IE0011支付宝二维码; IE0012支付宝网页; IE0013支付宝移动网页; IE0021微信二维码; IE0022微信移动网页.|
|sign       |string  |签名，签名规则 sign md5($mid.$pay\_type.$out\_trade\_no.$api\_key)<br/>api_key 通过平台注册时获取|

#### 返回:

```
success:
	{
	    "is_success": "TRUE",
	    "message": "SUCCESS",
	    "extra": []
	}

fail:
	{
	    "is_success": "FALSE",
	    "message": "SIGN_ERROR",
	    "extra": []
	}
	{
	    "is_success": "FALSE",
	    "message": "COMBINE_ERROR",
	    "extra": []
	}
	{
	    "is_success": "TRUE",
	    "message": {
		"pay_type": "IE0022",
		"out_trade_no": "2018050803414613700000490",
		"order_status": "1"
	    },
	    "extra": []
	}
	
	## 返回 order_status状态， 0代表未支付, 1代表已支付, 2代表已退款， 3代表已结算， 4代表结算了并且退款
```
