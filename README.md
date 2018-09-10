Platron Atol SDK
===============
## Установка

Проект предполагает установку с использованием composer
<pre><code>...
    "repositories": [
        {
            "type": "git",
            "url": "https://github.com/d3v3r73e/atol-online"
        }
    ]
...</pre></code>

## Примеры использования

### 1. Запрос токена

```php
$client = new Platron\Atol\clients\PostClient();

$tokenService = new Platron\Atol\services\GetTokenRequest('login', 'password');
$tokenResponse = new Platron\Atol\services\GetTokenResponse($client->sendRequest($tokenService));
```

### 2. Создание чека

```php
$client = new Platron\Atol\clients\PostClient();
$receiptPosition = new Platron\Atol\data_objects\ReceiptPosition('Test product', 10.00, 2, Platron\Atol\data_objects\ReceiptPosition::TAX_VAT10);

$createDocumentService = (new Platron\Atol\services\CreateDocumentRequest('token'))
    ->addCustomerEmail('test@test.ru')
    ->addCustomerPhone('79268750000')
    ->addGroupCode('groupCode')
    ->addInn('inn')
    ->addMerchantAddress('paymentAddress')
    ->addOperationType(Platron\Atol\services\CreateDocumentRequest::OPERATION_TYPE_BUY)
    ->addPaymentType(Platron\Atol\services\CreateDocumentRequest::PAYMENT_TYPE_ELECTRON)
    ->addSno(Platron\Atol\services\CreateDocumentRequest::SNO_ESN)
    ->addExternalId('externalId')
    ->addReceiptPosition($receiptPosition);
$createDocumentResponse = new Platron\Atol\services\CreateDocumentResponse($client->sendRequest($createDocumentService));
```

### 3. Запрос статуса 

```php
$client = new Platron\Atol\clients\PostClient();
$getStatusService = new Platron\Atol\services\GetStatusRequest('groupCode', 'uuid', 'token');
$getStatusResponse = new Platron\Atol\services\GetStatusResponse($client->sendRequest($getStatusService));
```
