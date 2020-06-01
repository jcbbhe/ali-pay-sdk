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