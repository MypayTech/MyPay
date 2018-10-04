<p align="center">
<h3 align="center">MyPay —— PC线上支付</h3><hr>
</p>

```
这边提供的线上支付的网页，商户不需要进行额外太多开发，可同步返回和异步返回。
同步返回和异步的参数需要通过后台设置
```


#### 请求:

```
Method: HTTP GET

https://mypay.iemoney.co.nz/api/mypay_pc
```
|Parameter	|Type 	 |Description|
|-----------|--------|-----------|
|mid        |int     |5位数，这边获取注册|
|fee        |string  |最多两位小数的数值，如：200.65|
|trade_no   |string  |商户自己的订单号，32位，官方建议：时间日期，加随机数，唯一订单号|
|subject    |string  |商品描述|
|return_url |string  |同步回调|
|notify_url |string  |异步回调|

#### 返回:

```
一个完整的页面

前端pc直接跳转到这个url
example : 
https://mypay.iemoney.co.nz/api/mypay_pc?mid=10209&subject=test&fee=0.01&trade_no=20180125033932
```

#### 支付回调：
|Parameter	|Type 	 |Description|
|-----------|--------|-----------|
|trade_no   |string  |商户自己的订单号，32位，官方建议：时间日期，加随机数，唯一订单号|
|trade_status   |string  |订单的支付状态，成功返回“SUCCESS”|
|sign       |string  |签名，签名规则 sign md5($trade_no.$trade_status.$api_key) <br/>api_key 通过平台注册时获取|

```
同步返回：
https://return.url/?trade_no=20180125033932&trade_status=SUCCESS

异步返回：
https://callback.url/?trade_no=20180125033932&trade_status=SUCCESS&sign=04a05e0d54598ef01882c18da7992762

异步请求收到后，要输出"SUCCESS"，不然会一直重复发送异步通知

```
