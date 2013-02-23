## Usage

```php

// simple chained payment

$body = array(
  'actionType' => 'PAY',
  'cancelUrl' => 'http://google.com',
  'returnUrl' => 'http://yahoo.com',
  'currencyCode' => 'USD',
  'trackingId' => time(),
  'feesPayer' => 'EACHRECEIVER',
  'memo' => 'Pay up!',
);

$receivers = array();

$receiver = array();
$receiver['email'] = 'seller@gmail.com';
$amount = 100;
$receiver['amount'] = number_format($amount, 2, '.', ',');
$receiver['primary'] = true;
$receivers[] = $receiver; // add receiver to receivers list

$receiver = array();
$receiver['email'] = 'marketplace@gmail.com';
$amount = 10;
$receiver['amount'] = number_format($amount, 2, '.', ',');
$receiver['primary'] = false;
$receivers[] = $receiver; // add receiver to receivers list

// format receivers in weird PayPal format
foreach ($receivers as $index => $receiver){
	foreach ($receiver as $key => $value){
		$body['receiverList.receiver('.$index.').'.$key] = $value;
	}
}

$request = PayPal::Payments()->Pay($body);

if($request->success)
{
  // do something
}

```
