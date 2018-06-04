# weipay
1、微信H5支付
- 安装
```
composer require rxlisbest/weipay=~1.0.2
```
- 用法
```
use rxlisbest\weipay\H5;

$mchid = 'xxxxx';          //微信支付商户号 PartnerID 通过微信支付商户资料审核后邮件发送
$appid = 'xxxxx';  //微信支付申请对应的公众号的APPID
$appKey = 'xxxxx';   //微信支付申请对应的公众号的APP Key
$apiKey = 'xxxxx';   //https://pay.weixin.qq.com 帐户设置-安全设置-API安全-API密钥-设置API密钥
$outTradeNo = uniqid();     //你自己的商品订单号
$payAmount = 0.01;          //付款金额，单位:元
$orderName = '支付测试';    //订单标题
$notifyUrl = 'http://www.xxx.com/wx/notify.php';     //付款成功后的回调地址(不要有问号)
$wapUrl = 'www.xxx.com';   //WAP网站URL地址
$wapName = 'H5支付';       //WAP 网站名

/** 配置结束 */
$wxPay = new H5($mchid, $appid, $apiKey);
$wxPay->setTotalFee($payAmount);
$wxPay->setOutTradeNo($outTradeNo);
$wxPay->setOrderName($orderName);
$wxPay->setNotifyUrl($notifyUrl);
$wxPay->setWapUrl($wapUrl);
$wxPay->setWapName($wapName);
$mwebUrl= $wxPay->createJsBizPackage();
$url = json_decode(json_encode($mwebUrl), true)[0]);
$url .= '&redirect_url=' . urlencode('http://xxxxx'); // 支付成功后跳转
header('Location: ' . $url);
```
