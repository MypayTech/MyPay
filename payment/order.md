<p align="center">
<h3 align="center">MyPay —— 生成订单支付接口</h3><hr>
</p>




#### 请求:

```
Method: HTTP POST

https://mypay.iemoney.co.nz/api/online
```

|Parameter	|Type 	 |Description|
|-----------|--------|-----------|
|mid        |int     |5位数，这边获取注册|
|total_fee        |string  |金额, NZD, 以cent为单位，如：2005 = 20.05纽币
|rmb_fee        |string  |金额, RMB, 以人民币分为单位，如：2005= 20.05人民币, total_fee和rmb\_fee只能传递一个（Alipay）
|goods   |string(64)  |商品名字，不能含有特殊字符，必填|
|goods_detail   |string(128)  |商品描述，不能含有特殊字符，必填|
|out\_trade_no   |string  |商户自己的订单号，与pay_type的组合必须唯一，微信最多32位，支付宝最多64位，官方建议：时间日期，加随机数，唯一订单号. 必填|
|pay_type   |string  |支付方式: IE0011支付宝二维码; IE0012支付宝网页; IE0013支付宝移动网页; IE0021微信二维码; IE0022微信移动网页. 必填|
|expired    |int  |有效期, 单位为秒.默认3600 选填|
|return_url |string(512)  |同步回调url. 选填|
|notify_url |string(512)  |异步回调url. 选填|
|sign       |string  |签名，签名规则 sign md5($mid.$pay\_type.$out\_trade_no.$notify\_url.$api\_key)<br/>api\_key 通过平台注册时获取|


#### 返回:

```
{
    "is_success": "TRUE",
    "message": "weixin://wxpay/bizpayurl?pr=uD61Ba3",
    "extra": []
}

{
    "is_success": "TRUE",
    "message": "alipay://wxpay/bizpayurl?pr=MPsO2Nu",
    "extra": []
}

{
    "is_success": "FALSE",
    "message": "SIGN_ERROR",
    "extra": []
}
 
{
    "is_success": "FALSE",
    "message": "ORDER_CREATED",
    "extra": {
        "mid": "10209",
        "pay_url": "weixin://wxpay/bizpayurl?pr=MPsO2Nu",
        "pay_type": "IE0021",
        "out_trade_no": "22322132122323121115222"
    }
}

```

#### 支付结果同步通知:

```
支付成功后，会同步返回通知：
$url = $notify_url."?out_trade_no=".$out_trade_no."&trade_status=SUCCESS&pay_type=".$pay_type."&sign=".$sign;

$sign = md5($out_trade_no.$pay_type.$api_key);

举个栗子🌰：

http://www.test.com?out_trade_no=2123123213d213233d1212131b&trade_status=SUCCESS&pay_type=IE0022&sign=198e7f765ccaebbc2157ce5e936ee1ff

⚠️注：同步返回是不可靠的，可能会由于网络原因比异步返回更快。只可用于UI显示交互的作用。不能用于结果的凭据。

```

#### 支付结果异步通知:

```
异步请求收到后，要输出"SUCCESS"，不然会一直重复发送异步通知，持续发送时间间隔不断增大。

注：可能会在一开始的时候，就一次性发送两条通知。商户需注意订单号的唯一性。

异步请求返回：

$url = $notify_url."?out_trade_no=".$out_trade_no."&trade_no=".$trade_no."&trade_status=SUCCESS&pay_type=".$pay_type."&sign=".$sign;

$sign = md5($trade_no.$out_trade_no.'SUCCESS'.$api_key);

举个栗子🌰：

http://www.test.com?out_trade_no=2123123213d213233d1212131b&trade_no=2018050421001003210531923654&trade_status=SUCCESS&pay_type=IE0012&sign=198e7f765ccaebbc2157ce5e936ee1ff
```

#### 🏄 有任何接入的问题可以随时联系MyPay这边的技术人员。随时回复，协助开发。😊

