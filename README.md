# ali-pay-sdk
```
composer require jcbbhe/alipay
```

# Query 订单查询

```
use AliPay\Bean\BaseContent;
 use AliPay\Bean\Query;
 use AliPay\Factory;
 
 require_once 'function.php';
 require_once '../vendor/autoload.php';
 
 
 Factory::$config = getAliPayConfig();
 
 $baseContent = new BaseContent('alipay.trade.query');
 $bizContent = new Query();
 $bizContent->trade_no = '2020053022001445941403725960';
 $baseContent->biz_content = $bizContent;
 try {
     $result = Factory::exec($baseContent);
 } catch (Exception $e) {
 }
 dump($result);
```

# 手机网站支付

```
require_once 'function.php';
require_once '../vendor/autoload.php';

use AliPay\Bean\BaseContent;
use AliPay\bean\GoodsDetail;
use AliPay\bean\WapPay;
use AliPay\Factory;


Factory::$config = getAliPayConfig();

$baseContent = new BaseContent('alipay.trade.wap.pay');
$baseContent->return_url = '';
$baseContent->notify_url = '';

$wapPay = new WapPay();
$wapPay->subject = '娃哈哈';
$wapPay->out_trade_no = 'd5d35c62-fd7c-4905-bcca-c9aa2e167e9a';
$wapPay->quit_url = 'https://www.baidu.com';

$totalAmount = 0;
for ($i = 0; $i < 3; $i++) {
    $goodsDetails = new GoodsDetail();
    $goodsDetails->goods_id = '122';
    $goodsDetails->goods_name = '矿泉水';
    $goodsDetails->quantity = 1;
    $goodsDetails->price = 0.01;
    $currentAmount = bcmul($goodsDetails->price, $goodsDetails->quantity, 2);
    $totalAmount = bcadd($totalAmount, $currentAmount, 2);
    $wapPay->addGoodsDetail($goodsDetails);
}
$wapPay->total_amount = $totalAmount;
$baseContent->biz_content = $wapPay->result();
try {
    $result = Factory::create($baseContent);
    dump($result);
} catch (Exception $e) {
}
```