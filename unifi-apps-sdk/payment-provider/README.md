---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/unifi-apps-sdk/payment-provider
---

# Payment Provider

## 01. Payment Flow

### Flowchart

#### Polling

<figure><img src="../../.gitbook/assets/스크린샷 2026-01-27 오후 2.32.29.png" alt=""><figcaption></figcaption></figure>

#### Webhook

<figure><img src="../../.gitbook/assets/스크린샷 2026-01-27 오후 2.35.35.png" alt=""><figcaption></figcaption></figure>

#### 1. Triggering createPayment API from Unifi Apps

When a user requests a purchase, the <mark style="background-color:purple;">Unifi App Client</mark> sends the item information to the <mark style="background-color:purple;">Unifi App Server</mark>.\
The <mark style="background-color:purple;">Unifi App Server</mark> then calls the `createPayment` API on the <mark style="background-color:green;">Unifi Payment Server</mark>.\
The `createPayment` API responds with a payment ID in the format: `{ id: <payment_id> }`.

**Request**

```bash
curl --location 'https://payment.dappportal.io/api/payment-v1/payment/create' \
--header 'X-Client-Id: {your_client_id}' \
--header 'X-Client-Secret: {your_client_secret}' \
--header 'Content-Type: application/json' \
--data '{
    "buyerDappPortalAddress": "{user_wallet_address}", // user_wallet_address should be achieved through walletProvider.
    "pgType": "{pg_type}",
    "currencyCode": "{currency_code}",
    "price": "{price}",
    "paymentStatusChangeCallbackUrl": "{url_to_get_confirm_callback}",
    "lockUrl": "{url_to_get_item_lock_callback}",
    "unlockUrl": "{url_to_get_item_unlock_callback}",
    "items": [
        {
            "itemIdentifier": "{your_item_identifier}",
            "name": "{your_item_name}",
            "imageUrl": "{your_item_image_url}",
            "price": "{price}",
            "currencyCode": "{currencyCode}"
        }
    ],
    "testMode": {true | false}
}'
```

**Response**

```
{
    "id": {payment_id}
}
```

#### 2. Get paymentProvider from sdk instance.

The <mark style="background-color:purple;">Unifi App Client</mark> retrieves the `PaymentProvider` instance from sdk with getPaymentProvider method.

```javascript
const paymentProvider = sdk.getPaymentProvider()
```

#### 3. Start payment process via paymentProvider.&#x20;

Then, call the `startPayment` method of the `paymentProvider`, passing the `paymentId` received from step 1 as a parameter.

```javascript
await paymentProvider.startPayment(paymentId)
```

#### 4. Check payment status and finalize payment.

There are two ways to check the payment status:

**Client-side**: Wait for the promise returned by the `startPayment` method to resolve. When the promise resolves, the payment status is updated to `FINALIZED`

**Server-side**: Handle the payment status via a webhook event on the server.\
When using webhooks, the <mark style="background-color:green;">Unifi Payment Server</mark> sends an update to the `paymentStatusChangeCallbackUrl` specified in the parameters of the `createPayment` API whenever the payment status changes. \
The update request is sent as an HTTP <mark style="background-color:green;">POST</mark> , and the body includes the updated payment status in the following format:

```json
{
  "paymentId": "{payment_id}",
  "status": "CONFIRMED"
}
```

If the received `status` is `CONFIRMED`, the <mark style="background-color:purple;">Mini Dapp Server</mark> should send a request to finalize the payment by calling the following API:

```bash
curl --location --request 
POST 'https://payment.dappportal.io/api/payment-v1/payment/finalize' \
--header 'Content-Type: application/json' \
--data '{
    "id": "{payment_id}"
}'
```

#### 5. In case of payment canceled by system.

If an HTTP `200 OK` status is not returned in response to the webhook event, the event will be retried up to four times at exponential intervals: **1, 2, 4, and 8 seconds**.

After all retry attempts have failed, if a `lockUrl` was specified when the payment was created, the <mark style="background-color:green;">Unifi Payment Server</mark> will send an unlock request as an HTTP <mark style="background-color:green;">POST</mark> . The body includes the paymentId and itemIdentifiers.

```json
{
    "paymentId": "{payment_id}",
    "itemIdentifiers": ["{your_item_identifier}"]
}
```

This ensures that any reserved resources (e.g., NFT items, inventory) are released properly in case the payment status could not be confirmed via webhook.

#### 6. You can open payment history page via paymentProvider. Promise will be completed if payment history page opens successfully.

```javascript
await paymentProvider.openPaymentHistory()
```

## 02. Payment API

baseUrl for Payment API:  https://payment.dappportal.io

### 1. create payment

&#x20;<mark style="background-color:green;">**post**</mark>**&#x20;  /api/payment-v1/payment/create**\
\
**Parameters**

| Name                                                                                                | Description                               |
| --------------------------------------------------------------------------------------------------- | ----------------------------------------- |
| <p>X-Client-Id <mark style="color:red;">*required</mark><br>string<br><em>(header)</em></p>         | client id obtained from support team      |
| <p>X-Client-Secret <mark style="color:red;">*required</mark><br>string<br><em>(header)</em><br></p> | client secret obtained from support team  |

**Request Body**

<table data-full-width="false"><thead><tr><th>Example Value</th><th>Schema</th></tr></thead><tbody><tr><td><pre class="language-javascript"><code class="lang-javascript">{
<strong>    "buyerDappPortalAddress": "{user_wallet_address}",
</strong>    "pgType": "{pg_type}",
    "currencyCode": "{currency_code}",
    "price": "{price}",
    "paymentStatusChangeCallbackUrl": "{url_to_get_status_change_callback_using_webhook}",
    "lockUrl": "{url_to_get_item_lock_callback}",
    "unlockUrl": "{url_to_get_item_unlock_callback}",
    "items": [
        {
            "itemIdentifier": "{your_item_identifier}",
            "name": "{your_item_name}",
            "imageUrl": "{your_item_image_url}",
            "price": "{price}",
            "currencyCode": "{currencyCode}"
        }
    ],
    "testMode": {true | false}
}
</code></pre></td><td><pre class="language-javascript"><code class="lang-javascript">{
    buyerDappPortalAddress*: String,
    pgType*: String(Enum: [STRIPE,CRYPTO]),
<strong>    currencyCode*: String(Enum: [USD,KRW,JPY,TWD,THB,KAIA,USDT]),
</strong>    price*: String,
    paymentStatusChangeCallbackUrl*: String,
    lockUrl: String,
    unlockUrl: String,
    items*: [Item {
           itemIdentifier: String,
           name: String,
           imageUrl: String,
           price: String,
           currencyCode: String(Enum: [USD,KRW,JPY,TWD,THB,KAIA,USDT]),
        }],
    testMode*: Boolean,
}
</code></pre></td></tr></tbody></table>

<table data-full-width="false"><thead><tr><th width="260">field</th><th>limitation</th></tr></thead><tbody><tr><td>buyerDappPortalAddress</td><td>Max length : 42</td></tr><tr><td>pgType</td><td><ul><li>STRIPE</li><li>CRYPTO</li></ul></td></tr><tr><td>currencyCode</td><td><ul><li>USD</li><li>KRW</li><li>JPY</li><li>TWD</li><li>THB</li><li>KAIA</li><li>USDT</li></ul><p>It should be equal to Item's currencyCode</p></td></tr><tr><td>price</td><td><ul><li><p>STRIPE</p><ul><li><p>Put minimum unit following <a href="https://en.wikipedia.org/wiki/ISO_4217">here</a></p><ul><li>100(cent) should be put if price is $1 </li></ul></li><li><p>Case1. Minumum unit equals to price unit</p><ul><li>10,000 KRW = 10000</li><li>10,000 JPY = 10000</li></ul></li><li><p>Case2. Minimum unit no equals to price unit</p><ul><li>10,000 USD = 1000000 (10,000 * 100)</li><li>10,000 THB = 1000000 (10,000 * 100)</li><li>10,000 TWD = 1000000 (10,000 * 100)</li></ul></li></ul></li><li><p>CRYPTO</p><ul><li><p>KAIA</p><ul><li>Put price as KAIA unit</li><li>1 KAIA = 1.0</li><li>Up to 4 demcimal places</li></ul></li><li><p>USDT</p><ul><li>1 USDT = 1.0</li><li>Up to 2 decimal places</li></ul></li></ul></li></ul><p></p><p>It should be equal to sum of each price of Items.<br><br>- Decimal Policy<br>STRIPE : no</p></td></tr><tr><td>paymentStatusChangeCallbackUrl<br><a href="./#id-3.-payment-status-change-event">for more detail</a></td><td><p>Max length : 512<br><br>You can receive webhook whenever payment status was changed if you set paymentStatusChangerCallbackUrl. </p><p><mark style="color:red;">Please use port 443 for entire connection. Webhooks cannot be received if a port other than 443 is used.</mark></p></td></tr><tr><td>lockUrl<br><a href="./#id-1.-lock-event">for more detail</a></td><td>Max length : 512</td></tr><tr><td>unlockUrl<br><a href="./#id-2.-unlock-event">for more detail</a></td><td>Max length : 512</td></tr><tr><td>items(*)</td><td>Only the purchase of single item is supported under current version</td></tr><tr><td>testMode</td><td>The payment methods according to testMode are as follows.<br><br>- testMode : false<br>stripe : realmode<br>crypto : kaia<br>- testMode : true<br>stripe : testmode<br>crypto : kairos</td></tr></tbody></table>

Items(\*)

<table><thead><tr><th width="182">field</th><th>limitation</th></tr></thead><tbody><tr><td>itemIdentifier</td><td>Max length : 256</td></tr><tr><td>name</td><td>Max length : 256</td></tr><tr><td>imageUrl</td><td>Max length : 512</td></tr><tr><td>price</td><td><p>Put minimum unit following <a href="https://en.wikipedia.org/wiki/ISO_4217">here</a></p><p>For example, put 100(cent) if price is 1 Dollar.</p></td></tr><tr><td>currencyCode</td><td><ul><li>USD</li><li>KRW</li><li>JPY</li><li>TWD</li><li>THB</li><li>KAIA</li><li>USDT</li></ul></td></tr></tbody></table>

\
**Responses**

<table data-full-width="false"><thead><tr><th width="149.0745849609375">HTTP Status Code</th><th>description</th></tr></thead><tbody><tr><td>200</td><td><p>Example Value</p><pre class="language-javascript"><code class="lang-javascript">{
    "payment_id": "{payment_id}"
}
</code></pre><p>Schema</p><pre class="language-javascript"><code class="lang-javascript">{
    payment_id*: String
}
</code></pre></td></tr><tr><td>400</td><td><p>Example Value</p><pre class="language-javascript"><code class="lang-javascript">{
    "code": 1001,
    "detail": "Invalid argument",
    "cause": null
}
</code></pre><p>Schema</p><pre class="language-javascript"><code class="lang-javascript">{    
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>401</td><td><p>Example Value</p><pre class="language-javascript"><code class="lang-javascript">{
    "code": 1007,
    "detail": "Invalid X-Client-Id or X-Client-Secret",
    "cause": null
}
</code></pre><p>Schema</p><pre class="language-javascript"><code class="lang-javascript">{    
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>403</td><td><p>Example Value</p><pre class="language-javascript"><code class="lang-javascript">{
    "code": 1007,
    "detail": "Access denied due to country restrictions.",
    "cause": null
}
</code></pre><p>Schema</p><pre class="language-javascript"><code class="lang-javascript">{    
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>500</td><td><p>Example Value</p><pre class="language-javascript"><code class="lang-javascript">{
    "code": 500,
    "detail": "Internal server error",
    "cause": null
}
</code></pre><p>Schema</p><pre class="language-javascript"><code class="lang-javascript">{    
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr></tbody></table>

**Request Example**

```bash

curl --location 'https://payment.dappportal.io/api/payment-v1/payment/create' \
--header 'X-Client-Id: {your_client_id}' \
--header 'X-Client-Secret: {your_client_secret}' \
--header 'Content-Type: application/json' \
--data '{
    "buyerDappPortalAddress": "{user_wallet_address}",
    "pgType": "{pg_type}",
    "currencyCode": "{currency_code}",
    "price": "{price}",
    "paymentStatusChangeCallbackUrl": "{url_to_get_confirm_callback}",
    "lockUrl": "{url_to_get_item_lock_callback}",
    "unlockUrl": "{url_to_get_item_unlock_callback}",
    "items": [
        {
            "itemIdentifier": "{your_item_identifier}",
            "name": "{your_item_name}",
            "imageUrl": "{your_item_image_url}",
            "price": "{price}",
            "currencyCode": "{currencyCode}"
        }
    ],
    "testMode": {true | false}
}'
```

### 2. get payment information

&#x20;<mark style="background-color:blue;">**get**</mark>   **/api/payment-v1/payment/info**<br>

**Parameters**

| Name                                                                                                | Description                               |
| --------------------------------------------------------------------------------------------------- | ----------------------------------------- |
| <p>X-Client-Id <mark style="color:red;">*required</mark><br>string<br><em>(header)</em></p>         | client id obtained from support team      |
| <p>X-Client-Secret <mark style="color:red;">*required</mark><br>string<br><em>(header)</em><br></p> | client secret obtained from support team  |
| <p>id <mark style="color:red;">*required</mark></p><p>string<br><em>(query)</em></p>                | payment id                                |

**responses**

<table data-full-width="false"><thead><tr><th width="146.04241943359375">HTTP Status Code</th><th>Description</th></tr></thead><tbody><tr><td>200</td><td><p>Example Value</p><pre class="language-javascript"><code class="lang-javascript">{
    "id":"{payment id}",
    "buyerDappPortalAddress": "{user_wallet_address}",
    "pgType": "{pg_type}",
    "status": "{status}",
    "currencyCode": "{currency_code}",
    "price": "{price}",
    "usdExchangeRate":"{Fx rate at the completion of payment. It is only returned where pgType is STRIPE and status is CONFIRMED or FINALIZED.}",
    "usdExchangePrice":"{USD Price applied fx rate at the completion of payment. It is only returned where pgType is STRIPE and status is CONFIRMED or FINALIZED."}
    "items": [
        {
            "itemIdentifier": "{your_item_identifier}",
            "name": "{your_item_name}",
            "imageUrl": "{your_item_image_url}",
            "price": "{price}",
            "currencyCode": "{currencyCode}"
        }
    ],
    "testMode": {true | false},
    "refund": {
      type: "REFUND",
      amount: "1000.0000000000000000000000000000", //Price policy follows . 
    }
}
</code></pre><p><br>Schema</p><pre><code>{
    id*: String,     
    buyerDappPortalAddress*: string(maxLength: 42),
    pgType*: string(Enum: [STRIPE,CRYPTO]),
    status*: string(Enum: [CREATED,STARTED,REGISTERED_ON_PG,CAPTURED,CONFIRMED,CONFIRM_FAILED,FINALIZED,CANCELED])
    currencyCode*: string(Enum: [USD,KRW,JPY,TWD,THB,KAIA,USDT]),
    price*: string,
    usdExchangeRate: string,
    usdExchangePrice: string,
    items*: [Item {
           itemIdentifier: string(maxLength: 256),
           name: string(maxLength: 256),
           imageUrl: string(maxLength: 512),
           price: string,
           currencyCode: string(Enum: [USD,KRW,JPY,TWD,THB,KAIA,UDST]),
        }]    
    testMode*: Boolean,
    refund: {
           type*: string(Enum:[CHARGEBACK, REFUND]),
           amount*: string,
           chargebackStatus: string(Enum:[NEEDS_RESPONSE, UNDER_REVIEW, WON, LOSE]), 
    }
}
</code></pre></td></tr><tr><td>404</td><td><p>Example Value</p><pre><code>{
    "code": 1002,
    "detail": "Not found payment",
    "cause": null
}
</code></pre><p>Schema</p><pre><code>{
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>401</td><td><p>Example Value</p><pre><code>{
    "code": 1007,
    "detail": "Invalid X-Client-Id or X-Client-Secret Header is not included when payment status is CONFIRMED or FINALIZED.",
    "cause": null
}
</code></pre><p>Schema</p><pre><code>{
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>403</td><td><p>Example Value</p><pre><code>{
    "code": 4030,
    "detail": "Access denied due to country restrictions.",
    "cause": null
}
</code></pre><p>Schema</p><pre><code>{
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>500</td><td><p>Example Value</p><pre><code>{
    "code": 500,
    "detail": "Internal server error",
    "cause": null
}
</code></pre><p>Schema</p><pre><code>{
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr></tbody></table>

<table data-full-width="false"><thead><tr><th width="230.6944580078125">field</th><th>limitation</th></tr></thead><tbody><tr><td>id</td><td></td></tr><tr><td>buyerDappPortalAddress</td><td>Max length : 42</td></tr><tr><td>pgType</td><td><ul><li>STRIPE</li><li>CRYPTO</li></ul></td></tr><tr><td>status</td><td><p>Payment status ><br></p><ul><li>CREATED</li><li>STARTED</li><li>REGISTERED_ON_PG</li><li>CAPTURED</li><li>CONFIRMED</li><li>CONFIRM_FAILED</li><li>FINALIZED</li><li>CANCELED</li><li>REFUNDED</li><li>CHARGEBACK</li></ul></td></tr><tr><td>currencyCode</td><td><ul><li>USD</li><li>KRW</li><li>JPY</li><li>TWD</li><li>THB</li><li>KAIA</li><li>USDT</li></ul><p>It should be equal to Item's currencyCode</p></td></tr><tr><td>price</td><td>Put minimum unit as <a href="https://en.wikipedia.org/wiki/ISO_4217">here</a>. <br>For example, put 100(cent) if price is 1 Dollar. It should be equal to sum of each price of Items.<br><br>- Decimal Policy<br>STRIPE : no<br>CRYPTO : Up to 4 decimal places</td></tr><tr><td>usdExchangeRate</td><td>Fx rate at the completion of payment. It is only returned where pgType is STRIPE and status is CONFIRMED or FINALIZED.</td></tr><tr><td>usdExchangePrice</td><td>USD Price applied fx rate at the completion of payment. It is only returned where pgType is STRIPE and status is CONFIRMED or FINALIZED.</td></tr><tr><td>items(*)</td><td>Only the purchase of single item is supported under current version</td></tr><tr><td>testMode</td><td>The payment methods according to testMode are as follows.<br><br>- testMode : false<br>stripe : realmode<br>crypto : kaia<br>- testMode : true<br>stripe : testmode<br>crypto : kairos</td></tr><tr><td>refund</td><td></td></tr><tr><td>refund.type</td><td><ul><li>CHARGEBACK</li><li>REFUND</li></ul></td></tr><tr><td>refund.amount</td><td>Price policy follows <a href="https://en.wikipedia.org/wiki/ISO_4217">here</a>. </td></tr><tr><td>refund.chargebackStatus</td><td><ul><li>NEEDS_RESPONSE: A CHARGEBACK has occurred, but it is in the state before contesting or challenging it.</li><li>UNDER_REVIEW: The dispute has been filed and is currently under review by STRIPE.</li><li>WON: If the dispute is accepted.</li><li>LOST: If the dispute result is not accepted</li></ul></td></tr></tbody></table>

Items(\*)

<table><thead><tr><th width="149.02886962890625">field</th><th>limitation</th></tr></thead><tbody><tr><td>itemIdentifier</td><td>Max length : 256</td></tr><tr><td>name</td><td>Max length : 256</td></tr><tr><td>imageUrl</td><td>Max length : 512</td></tr><tr><td>price</td><td>For example, put 100(cent) if price is 1 Dollar.</td></tr><tr><td>currencyCode</td><td><ul><li>USD</li><li>KRW</li><li>JPY</li><li>TWD</li><li>THB</li><li>KAIA</li><li>USDT</li></ul></td></tr></tbody></table>

**Request Example**

```bash
curl --location 'https://payment.dappportal.io/api/payment-v1/payment/info?id={payment_id}' \
--header 'X-Client-Id: {your_client_id}' \
--header 'X-Client-Secret: {your_client_secret}'
```

### 3. get payment status

&#x20;<mark style="background-color:blue;">**get**</mark>   **/api/payment-v1/payment/status**\
\
**Parameters**

| Name                                                                                 | Description |
| ------------------------------------------------------------------------------------ | ----------- |
| <p>id <mark style="color:red;">*required</mark></p><p>string<br><em>(query)</em></p> | payment id  |

**Responses**

<table><thead><tr><th width="145.7642822265625">HTTP Status Code</th><th>Description</th></tr></thead><tbody><tr><td>200</td><td><p>Example Value</p><pre class="language-javascript"><code class="lang-javascript">{
    "status": "{status}"
}
</code></pre><p>Schema</p><pre class="language-javascript"><code class="lang-javascript">{
    status*: String (Enum:[CREATED, STARTED, REGISTERED_ON_PG, CAPTURED, CONFIRMED_FAILED,FINALIZED,CANCELED]
}
</code></pre></td></tr><tr><td>403</td><td><p>Example Value</p><pre class="language-javascript"><code class="lang-javascript">{
    "code": 4030,
    "detail": "Access denied due to country restrictions.",
    "cause": null
}
</code></pre><p>Schema</p><pre class="language-javascript"><code class="lang-javascript">{
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>404</td><td><p>Example Value</p><pre class="language-javascript"><code class="lang-javascript">{
    "code": 1002,
    "detail": "Not found payment",
    "cause": null
}
</code></pre><p>Schema</p><pre class="language-javascript"><code class="lang-javascript">{
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>500</td><td><p>Example Value</p><pre class="language-javascript"><code class="lang-javascript">{
    "code": 500,
    "detail": "Internal server error",
    "cause": null
}
</code></pre><p>Schema</p><pre class="language-javascript"><code class="lang-javascript">{
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr></tbody></table>

<table data-full-width="false"><thead><tr><th>field</th><th>limitation</th></tr></thead><tbody><tr><td>status</td><td><p>Payment status ></p><ul><li>CREATED</li><li>STARTED</li><li>REGISTERED_ON_PG</li><li>CAPTURED</li><li>CONFIRMED</li><li>CONFIRMED_FAILED</li><li>FINALIZED</li><li>CANCELED</li><li>REFUNDED</li><li>CHARGEBACK</li></ul></td></tr></tbody></table>

**Request Example**

```bash
curl --location 'https://payment.dappportal.io/api/payment-v1/payment/status?id={payment_id}'
```

### 4. finalized payment

It will be ready to be settlement after requesting finalize payment API.

You can't get settlement for STRIPE transaction if you did not request finalize payment API.\
\
For CRYPTO, We recomment to request finalize payment API too.\
\
**Parameters** \
\
N/A

**Request Body**

<table><thead><tr><th>Example Value</th><th>Schema</th></tr></thead><tbody><tr><td><p></p><pre class="language-javascript"><code class="lang-javascript">{
    id: "{payment_id}" 
}
</code></pre></td><td><p></p><pre class="language-javascript"><code class="lang-javascript">{
    id*: String
}
</code></pre></td></tr></tbody></table>

**Responses**

<table><thead><tr><th width="159.82525634765625">HTTP Status Code</th><th>Description</th></tr></thead><tbody><tr><td>200</td><td>N/A</td></tr><tr><td>403</td><td><p>Example Value</p><pre class="language-javascript"><code class="lang-javascript">{
    "code": 1004,
    "detail": "Invalid payment status.",//Current payment status cannot complete payment finalization
    "cause": null
}
</code></pre><p>Schema</p><pre class="language-javascript"><code class="lang-javascript">{    
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>403</td><td><p>Example Value</p><pre class="language-javascript"><code class="lang-javascript">{
    "code": 4030,
    "detail": "Access denied due to country restrictions.",
    "cause": null
}
</code></pre><p>Schema</p><pre class="language-javascript"><code class="lang-javascript">{    
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>404</td><td><p>Example Value</p><pre class="language-javascript"><code class="lang-javascript">{
    "code": 1002,
    "detail": "Not found payment",
    "cause": null
}
</code></pre><p>Schema</p><pre class="language-javascript"><code class="lang-javascript">{    
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>500</td><td><p>Example Value</p><pre class="language-javascript"><code class="lang-javascript">{
    "code": 500,
    "detail": "Internal server error",
    "cause": null
}
</code></pre><p>Schema</p><pre class="language-javascript"><code class="lang-javascript">{    
    code*: number,
    detail*: String,
    cause: String

</code></pre></td></tr></tbody></table>

**Request Example**

```bash
curl --location 'https://payment.dappportal.io/api/payment-v1/payment/finalize
--header 'Content-Type: application/json' \
  --data '{
    "id": "{payment_id}"
  }
```

## 03. PaymentProvider

### sdk.getPaymentProvider()

Initializes the `paymentProvider`, allowing developers to use various payment features.

```javascript
const walletProvider = sdk.getWalletProvider();
```

#### Parameters

N/A

#### Responses

```
PaymentProvider
```

### paymentProvider.startPayment()

Calling `paymentProvider.startPayment()` displays a transaction window to the user and begins the payment process.

#### Parameters

payment\_id <mark style="color:red;">\*required</mark> · <mark style="color:green;">string</mark>

#### Responses

```javascript
Promise<unknown>
```

#### Error

<table><thead><tr><th>Code</th><th>Description</th></tr></thead><tbody><tr><td>-31001</td><td><p>This error is triggered when a <strong>STRIPE</strong> payment gets canceled.</p><pre class="language-json"><code class="lang-json">{
code: -31001,
message:'Payment is canceled by user or timeout'
}
</code></pre></td></tr><tr><td>-31002</td><td><pre class="language-json"><code class="lang-json">{
code: -31002,
message:'Payment is failed'
}
</code></pre></td></tr><tr><td>-32001</td><td><p>This error is triggered when a <strong>CRYPTO</strong> payment gets canceled.</p><pre class="language-json"><code class="lang-json">{
code: -32001,
message:'User denied transaction send.'
}
</code></pre></td></tr></tbody></table>

### paymentProvider.openPaymentHistory()

This method opens a payment history window. In order to complete the operation, a signature from the user is required.

#### Parameters

N/A

#### Responses

```
Promise<void>
```

## 04. Payment Webhook

Each Webhook's callback URL should be set differently.&#x20;

If `lockUrl` and `unlockUr` is not needed, please enter `null`.

### 1. lock event

`lockUrl` is a server endpoint that is called to temporarily lock or reserve the item being purchased. This is typically required for items with **limited quantity** or **NFTs**, to prevent overselling and ensure that no other user can purchase the item while the current payment is in progress.

If the `lockUrl` parameter is included in the create payment request, a POST method request for the lock webhook event will be made.

When the payment is initiated using the SDK’s startPayment function, the webhook event is requested just before starting the user’s payment flow if it is determined that the payment can proceed normally.

If a request is made with the `lockUrl` but a 200 response is not received, the payment will be immediately canceled and marked as failed automatically.

```
{
    "paymentId": "{payment_id}",
    "itemIdentifiers": [
        {
            "{your_item_identifier}"
        }
    ]
}
```

### 2. unlock event

`unlockUrl` is a server endpoint that is called when **a payment fails, is canceled, or times out**, in order to release the previously locked item and make it available for others to purchase again.

If the `unlockUrl` parameter is included in the **create payment request**, a `POST` request will be sent to this endpoint when a payment failure-related event is triggered.

If the payment is successfully completed (`status === CONFIRMED`), the `unlockUrl` **will not be called**.\
Instead, the item is typically **finalized** via a separate process (`finalize` API or internal logic).



&#x20;If a request is made with the `unlockUrl` but a 200 response is not received, it will be retried up to 5 times at intervals of 1, 2, 4 and 8 seconds. To avoid that the item remains locked, implementing background job to attempt unlocking again is recommended.&#x20;

```
{
    "paymentId": "{payment_id}",
    "itemIdentifiers": [
        {
            "{your_item_identifier}"
        }
    ]
}
```

### 3. payment status change event

When creating a payment request, a payment status change webhook event will be sent to the `paymentStatusChangeCallbackUrl` you've provided.

An event occurs whenever the payment status changes, except when the status is **CREATED**.

If the status of the received webhook is **CONFIRMED**, you can call the finalize payment API.

If a request to the paymentStatusChangeCallbackUrl does not receive a 200 response, a maximum of 5 retries will be made at intervals of 1, 2, 4, and 8 seconds. Even if a 200 response is not received after 5 retries, the payment cancellation will not proceed.

```
{
    "paymentId": "{payment_id}"
    "status": "STARTED|REGISTERED_ON_PG|CAPTURED_CONFIRMED_CONFIRM_FAILED|FINALIZED|CANCELED|REFUNDED|CHARGEBACK"
    "cryptoPaymentInfo": { // added when "status" is CONFIRMED
        "paymentTxHash": "0x.."
        }
}
```

<table data-full-width="false"><thead><tr><th width="527">Status</th><th>Description</th></tr></thead><tbody><tr><td>CREATED</td><td>Hosted create payment API but not host startPayment of SDK</td></tr><tr><td>STARTED</td><td>Hosted startPayment but await payment approval from user (STRIPE/CRYPTO)</td></tr><tr><td>REGISTERED_ON_PG</td><td>(Only for pgType = CRYPTO) <br>Transaction has been approved but await for enough block confirmation to prevent chain re-organization.<br>- at least after 10 block confirmation from user's request for KAIA</td></tr><tr><td>CAPTURED</td><td>(Only for pgType = CRYPTO)<br>Checking validity of the transaction after 10 blocks have confirmed from the user's transaction request</td></tr><tr><td>CONFIRMED</td><td>Payment approval is completed and await payment finalization from Mini Dapp</td></tr><tr><td>CONFIRM_FAILED</td><td>(Only for pgTye = CRYPTO)<br>Failed to check validity of the transaction after 10 blocks have confirmed from user's transaction request</td></tr><tr><td>FINALIZED</td><td>Payment process is done with paymet approval and payment finialization from Mini Dapp<br>- In case of pgType is CRYPTO, transactions will be automatically finalized after 5 minutes once it reachs the CONFIRMED status if the finalize payment API is not hosted.</td></tr><tr><td>CANCELED</td><td>Payment is cancelled as Policy for payment cancellation</td></tr><tr><td>REFUNDED</td><td>Payment has been refunded</td></tr><tr><td>CHARGEBACK</td><td><p>Users has claimed chargeback directly. </p><p>This Webhook message will be sent at each stage of the process, including the occurrence of a CHARGEBACK.</p></td></tr></tbody></table>

(\*) This status can only be queried through the get payment information API.

