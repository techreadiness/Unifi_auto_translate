# 결제

## 01. 결제 흐름

### 흐름도

#### 폴링

<figure><img src="../../../.gitbook/assets/SDK_Polling.png" alt=""><figcaption></figcaption></figure>#### 웹훅

<figure><img src="../../../.gitbook/assets/SDK_Webhook.png" alt=""><figcaption></figcaption></figure>

#### 1. 미니 앱에서 createPayment API 호출

사용자가 구매를 요청하면 <mark style="background-color:purple;">미니 앱 클라이언트가</mark> 아이템 정보를 <mark style="background-color:purple;">미니 앱 </mark>서버로 전송합니다.\
<mark style="background-color:purple;">미니 앱 </mark>서버는 <mark style="background-color:green;">Dapp Portal 결제 </mark>서버의 `createPayment` API를 호출합니다.\
`createPayment` API는 다음과 같은 형식의 결제 ID를 반환합니다: `{ id:<payment_id>

}`.

**요청**

```bash
curl --location &#x27;https://payment.dappportal.io/api/payment-v1/payment/create&#x27; \
--header &#x27;X-Client-Id: {your_client_id}&#x27; \
--header &#x27;X-Client-Secret: {your_client_secret}&#x27; \
--header &#x27;Content-Type: application/json&#x27; \
--data &#x27;{
    &quot;buyerDappPortalAddress&quot;: &quot;{user_wallet_address}&quot;, // user_wallet_address는 walletProvider를 통해 획득해야 합니다.
    &quot;pgType&quot;: &quot;{pg_type}&quot;,
    &quot;currencyCode&quot;: &quot;{currency_code}&quot;,
    &quot;price&quot;: &quot;{price}&quot;,
    &quot;paymentStatusChangeCallbackUrl&quot;: &quot;{확인 콜백을 받을 URL}&quot;,
    &quot;lockUrl&quot;: &quot;{아이템 잠금 콜백을 받을 URL}&quot;,
    &quot;unlockUrl&quot;: &quot;{아이템 잠금 해제 콜백을 받을 URL}&quot;,
    &quot;items&quot;: [
        {
            &quot;itemIdentifier&quot;: &quot;{your_item_identifier}&quot;,
            &quot;name&quot;: &quot;{your_item_name}&quot;,
            &quot;imageUrl&quot;: &quot;{your_item_image_url}&quot;,
            &quot;price&quot;: &quot;{price}&quot;,
            &quot;currencyCode&quot;: &quot;{currencyCode}&quot;
        }
    ],
    &quot;testMode&quot;: {true | false}
}&#x27;
```

**응답**

```
{
    &quot;id&quot;: {payment_id}
}
```

#### 2. SDK 인스턴스에서 PaymentProvider 가져오기.

<mark style="background-color:purple;">미니 Dapp</mark>

클라이언트는 getPaymentProvider 메서드를 통해 SDK에서 `PaymentProvider` 인스턴스를 가져옵니다.

```javascript
const paymentProvider = sdk.getPaymentProvider()
```

#### 3. paymentProvider를 통해 결제 프로세스 시작. 

그런 다음 `paymentProvider`의 `startPayment` 메서드를 호출하고, 1단계에서 받은 `paymentId`를 매개변수로 전달합니다.

```javascript
await paymentProvider.startPayment(paymentId)
```

#### 4. 결제 상태 확인 및 결제 완료 처리.

결제 상태를 확인하는 방법은 두 가지입니다:

**클라이언트 측**: `startPayment` 메서드가 반환한 프로미스가 해결될 때까지 대기합니다. 프로미스가 해결되면 결제 상태가 `FINALIZED`로 업데이트됩니다.

**서버 측**: 서버에서 웹훅 이벤트를 통해 결제 상태를 처리합니다.
웹훅을 사용할 경우, <mark style="background-color:green;">Dapp Portal 결제 서버는</mark>

결제 상태가 변경될 때마다 `createPayment` API 매개변수에 지정된 `paymentStatusChangeCallbackUrl`로 업데이트를 전송합니다.
업데이트 요청은 HTTP <mark style="background-color:green;">POST</mark>

로 전송되며, 본문에 다음과 같은 형식의 업데이트된 결제 상태가 포함됩니다:

```json
{
  &quot;paymentId&quot;: &quot;{payment_id}&quot;,
  &quot;status&quot;: &quot;CONFIRMED&quot;
}
```

수신된 `status`가 `CONFIRMED`인 경우, <mark style="background-color:purple;">미니 Dapp 서버는</mark>

다음 API를 호출하여 결제를 최종 확정하는 요청을 보내야 합니다:

```bash
curl --location --request 
POST &#x27;https://payment.dappportal.io/api/payment-v1/payment/finalize&#x27; \
--header &#x27;Content-Type: application/json&#x27; \
--data &#x27;{
    &quot;id&quot;: &quot;{payment_id}&quot;
}&#x27;
```

#### 5. 시스템에 의해 결제가 취소된 경우.

웹훅 이벤트에 대한 응답으로 HTTP `200 OK` 상태가 반환되지 않으면, 이벤트는 지수적으로 증가하는 간격(**1, 2, 4, 8초**)으로 최대 4회까지 재시도됩니다.

모든 재시도 실패 후, 결제 생성 시 `lockUrl`이 지정된 경우 <mark style="background-color:green;">Dapp Portal 결제 서버는</mark>

HTTP <mark style="background-color:green;">POST</mark>

로 잠금 해제 요청을 전송합니다. 본문에 paymentId와 itemIdentifiers가 포함됩니다.

```json
{
    &quot;paymentId&quot;: &quot;{payment_id}&quot;,
    &quot;itemIdentifiers&quot;: [&quot;{your_item_identifier}&quot;]
}
```

이는 웹훅을 통해 결제 상태를 확인할 수 없는 경우 예약된 리소스(예: NFT 아이템, 인벤토리)가 적절히 해제되도록 보장합니다.

#### 6. paymentProvider를 통해 결제 내역 페이지를 열 수 있습니다. 결제 내역 페이지가 성공적으로 열리면 Promise가 완료됩니다.

```javascript
await paymentProvider.openPaymentHistory()
```

## 02. 결제 API

결제 API 기본 URL:  https://payment.dappportal.io

### 1. 결제 생성

 <mark style="background-color:green;">**POST****</mark>

   /api/payment-v1/payment/create**\
\
**매개변수**

| 이름                                                                                                | 설명                               |
| --------------------------------------------------------------------------------------------------- | ----------------------------------------- |
|<p>X-Client-Id <mark style="color:red;">*필수</mark><br>문자열<br><em>(헤더)</em></p>

         | 지원팀으로부터 받은 클라이언트 ID      |
|<p>X-Client-Secret <mark style="color:red;">*필수</mark><br>문자열<br><em>(헤더)</em><br></p>

| 지원팀으로부터 받은 클라이언트 시크릿  |

**요청 본문**<table data-full-width="false"><thead><tr><th>예시 값</th><th>스키마</th></tr></thead><tbody><tr><td><pre class="language-javascript"><code class="lang-javascript">{
<strong>    &quot;buyerDappPortalAddress&quot;: &quot;{user_wallet_address}&quot;,
</strong>    &quot;pgType&quot;: &quot;{pg_type}&quot;,
    &quot;currencyCode&quot;: &quot;{currency_code}&quot;,
    &quot;price&quot;: &quot;{price}&quot;,
    &quot;paymentStatusChangeCallbackUrl&quot;: &quot;{url_to_get_status_change_callback_using_webhook}&quot;,
    &quot;lockUrl&quot;: &quot;{url_to_get_item_lock_callback}&quot;,
    &quot;unlockUrl&quot;: &quot;{url_to_get_item_unlock_callback}&quot;,
    &quot;items&quot;: [
        {
            &quot;itemIdentifier&quot;: &quot;{your_item_identifier}&quot;,
            &quot;name&quot;: &quot;{your_item_name}&quot;,
            &quot;imageUrl&quot;: &quot;{your_item_image_url}&quot;,
            &quot;price&quot;: &quot;{price}&quot;,
            &quot;currencyCode&quot;: &quot;{currencyCode}&quot;
        }
    ],
    &quot;testMode&quot;: {true | false}
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

<table data-full-width="false"><thead><tr><th width="260">필드</th><th>제한</th></tr></thead><tbody><tr><td>buyerDappPortalAddress</td><td>최대 길이 : 42</td></tr><tr><td>pgType</td><td><ul><li>STRIPE</li><li>CRYPTO</li></ul></td></tr><tr><td>통화 코드</td><td><ul><li>USD</li><li>KRW</li><li>JPY</li><li>TWD</li><li>THB</li><li>KAIA</li><li>USDT</li></ul><p>항목의 currencyCode와 동일해야 합니다.</p></td></tr><tr><td>가격</td><td><ul><li><p>STRIPE</p><ul><li><p><a href="https://en.wikipedia.org/wiki/ISO_4217">여기에</a> 최소 단위를 입력하세요</p><ul><li>가격이 1달러인 경우 100(센트)를 입력해야 함 </li></ul></li><li><p>Case1. 최소 단위가 가격 단위와 동일함</p><ul><li>10,000 KRW = 10000</li><li>10,000 JPY = 10000</li></ul></li><li><p>사례2. 최소 단위가 가격 단위와 다를 경우</p><ul><li>10,000 USD = 1000000 (10,000 * 100)</li><li>10,000 THB = 1000000 (10,000 * 100)</li><li>10,000 TWD = 1000000 (10,000 * 100)</li></ul></li></ul></li><li><p>암호화폐</p><ul><li><p>KAIA</p><ul><li>KAIA 단위로 가격 표시</li><li>1 KAIA = 1.0</li><li>소수점 이하 4자리까지</li></ul></li><li><p>USDT</p><ul><li>1 USDT = 1.0</li><li>소수점 이하 2자리까지</li></ul></li></ul></li></ul><p></p><p>항목의 각 가격의 합계와 같아야 합니다.<br><br>- 소수점 정책<br>STRIPE : 없음</p></td></tr><tr><td><a href="./#id-3.-payment-status-change-event">자세한 내용은</a> paymentStatusChangeCallbackUrl<br><a href="./#id-3.-payment-status-change-event">참조</a></td><td><p>최대 길이: 512 paymentStatusChangerCallbackUrl을<br><br>설정하면 결제 상태가 변경될 때마다 웹훅을 수신할 수 있습니다. </p><p><mark style="color:red;">전체 연결에 포트 443을 사용하십시오. 443 이외의 포트를 사용하는 경우 웹훅을 수신할 수 없습니다.</mark></p></td></tr><tr><td><a href="./#id-1.-lock-event">자세한 내용은</a> lockUrl을<br><a href="./#id-1.-lock-event">참조하십시오.</a></td><td>최대 길이 : 512</td></tr><tr><td><a href="./#id-2.-unlock-event">자세한 내용은</a> unlockUrl을<br><a href="./#id-2.-unlock-event">참조하십시오.</a></td><td>최대 길이 : 512</td></tr><tr><td>items(*)</td><td>현재 버전에서는 단일 항목 구매만 지원됩니다.</td></tr><tr><td>testMode</td><td>testMode에 따른 결제 방법은 다음과 같습니다.<br><br>- testMode : false<br>stripe : realmode<br>crypto : kaia<br>- testMode : true<br>stripe : testmode<br>crypto : kairos</td></tr></tbody></table>



항목(\*)

<table><thead><tr><th width="182">필드</th><th>제한 사항</th></tr></thead><tbody><tr><td>itemIdentifier</td><td>최대 길이 : 256</td></tr><tr><td>이름</td><td>최대 길이 : 256</td></tr><tr><td>imageUrl</td><td>최대 길이 : 512</td></tr><tr><td>가격</td><td><p>최소 단위를 <a href="https://en.wikipedia.org/wiki/ISO_4217">여기에</a> 입력하세요</p><p>예를 들어, 가격이 1달러인 경우 100(센트)를 입력하세요.</p></td></tr><tr><td>currencyCode</td><td><ul><li>USD</li><li>KRW</li><li>JPY</li><li>TWD</li><li>THB</li><li>KAIA</li><li>USDT</li></ul></td></tr></tbody></table>

\


<table data-full-width="false"><thead><tr><th width="149.0745849609375">HTTP 상태 코드</th><th>설명</th></tr></thead><tbody><tr><td>200</td><td><p>예시 값</p><pre class="language-javascript"><code class="lang-javascript">{
    &quot;payment_id&quot;: &quot;{payment_id}&quot;
}
</code></pre><p>스키마</p><pre class="language-javascript"><code class="lang-javascript">{
    payment_id*: String
}
</code></pre></td></tr><tr><td>400</td><td><p>예제 값</p><pre class="language-javascript"><code class="lang-javascript">{
    &quot;code&quot;: 1001,
    &quot;detail&quot;: &quot;Invalid argument&quot;,
    &quot;cause&quot;: null
}
</code></pre><p>스키마</p><pre class="language-javascript"><code class="lang-javascript">{    
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>401</td><td><p>예제 값</p><pre class="language-javascript"><code class="lang-javascript">{
    &quot;code&quot;: 1007,
    &quot;detail&quot;: &quot;Invalid X-Client-Id or X-Client-Secret&quot;,
    &quot;cause&quot;: null
}
</code></pre><p>스키마</p><pre class="language-javascript"><code class="lang-javascript">{    
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>403</td><td><p>예시 값</p><pre class="language-javascript"><code class="lang-javascript">{
    &quot;code&quot;: 1007,
    &quot;detail&quot;: &quot;Access denied due to country restrictions.&quot;,
    &quot;cause&quot;: null
}
</code></pre><p>스키마</p><pre class="language-javascript"><code class="lang-javascript">{    
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>500</td><td><p>예제 값</p><pre class="language-javascript"><code class="lang-javascript">{
    &quot;code&quot;: 500,
    &quot;detail&quot;: &quot;Internal server error&quot;,
    &quot;cause&quot;: null
}
</code></pre><p>스키마</p><pre class="language-javascript"><code class="lang-javascript">{    
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr></tbody></table>

**응답****요청 예시**

```bash

curl --location &#x27;https://payment.dappportal.io/api/payment-v1/payment/create&#x27; \
--header &#x27;X-Client-Id: {your_client_id}&#x27; \
--header &#x27;X-Client-Secret: {your_client_secret}&#x27; \
--header &#x27;Content-Type: application/json&#x27; \
--data &#x27;{
    &quot;buyerDappPortalAddress&quot;: &quot;{user_wallet_address}&quot;,
    &quot;pgType&quot;: &quot;{pg_type}&quot;,
    &quot;currencyCode&quot;: &quot;{currency_code}&quot;,
    &quot;price&quot;: &quot;{price}&quot;,
    &quot;paymentStatusChangeCallbackUrl&quot;: &quot;{url_to_get_confirm_callback}&quot;,
    &quot;lockUrl&quot;: &quot;{url_to_get_item_lock_callback}&quot;,
    &quot;unlockUrl&quot;: &quot;{url_to_get_item_unlock_callback}&quot;,
    &quot;items&quot;: [
        {
            &quot;itemIdentifier&quot;: &quot;{your_item_identifier}&quot;,
            &quot;name&quot;: &quot;{your_item_name}&quot;,
            &quot;imageUrl&quot;: &quot;{your_item_image_url}&quot;,
            &quot;price&quot;: &quot;{price}&quot;,
            &quot;currencyCode&quot;: &quot;{currencyCode}&quot;
        }
    ],
    &quot;testMode&quot;: {true | false}
}&#x27;
```

### 2. 결제 정보 가져오기

 <mark style="background-color:blue;">**</mark>

get

 <mark style="background-color:blue;">**</mark>

   <br>

**/api/payment-v1/payment/info**

**매개변수**

| 이름                                                                                                | 설명                               |
| --------------------------------------------------------------------------------------------------- | ----------------------------------------- |
|<p>X-Client-Id <mark style="color:red;">*필수</mark><br>문자열<br><em>(헤더)</em></p>

         | 지원팀으로부터 받은 클라이언트 ID      |
|<p>X-Client-Secret <mark style="color:red;">*필수</mark><br>문자열<br><em>(헤더)</em><br></p>

| 지원팀으로부터 받은 클라이언트 시크릿  |
|                <p>id <mark style="color:red;">*필수</mark></p><p>문자열<br><em>(쿼리)</em></p>

| 결제 ID                                |

<table data-full-width="false"><thead><tr><th width="146.04241943359375">HTTP 상태 코드</th><th>설명</th></tr></thead><tbody><tr><td>200</td><td><p>예제 값</p><pre class="language-javascript"><code class="lang-javascript">{
    &quot;id&quot;:&quot;{payment id}&quot;,
    &quot;buyerDappPortalAddress&quot;: &quot;{user_wallet_address}&quot;,
    &quot;pgType&quot;: &quot;{pg_type}&quot;,
    &quot;status&quot;: &quot;{status}&quot;,
    &quot;currencyCode&quot;: &quot;{currency_code}&quot;,
    &quot;price&quot;: &quot;{price}&quot;,
    &quot;usdExchangeRate&quot;:&quot;{Fx rate at the completion of payment. It is only returned where pgType is STRIPE and status is CONFIRMED or FINALIZED.}&quot;,
    &quot;usdExchangePrice&quot;:&quot;{USD Price applied fx rate at the completion of payment. It is only returned where pgType is STRIPE and status is CONFIRMED or FINALIZED.&quot;}
    &quot;items&quot;: [
        {
            &quot;itemIdentifier&quot;: &quot;{your_item_identifier}&quot;,
            &quot;name&quot;: &quot;{your_item_name}&quot;,
            &quot;imageUrl&quot;: &quot;{your_item_image_url}&quot;,
            &quot;price&quot;: &quot;{price}&quot;,
            &quot;currencyCode&quot;: &quot;{currencyCode}&quot;
        }
    ],
    &quot;testMode&quot;: {true | false},
    &quot;refund&quot;: {
      type: &quot;REFUND&quot;,
      amount: &quot;1000.0000000000000000000000000000&quot;, //Price policy follows . 
    }
}
</code></pre><p><br>스키마</p><pre><code>{
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
</code></pre></td></tr><tr><td>404</td><td><p>예제 값</p><pre><code>{
    &quot;code&quot;: 1002,
    &quot;detail&quot;: &quot;Not found payment&quot;,
    &quot;cause&quot;: null
}
</code></pre><p>스키마</p><pre><code>{
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>401</td><td><p>예시 값</p><pre><code>{
    &quot;code&quot;: 1007,
    &quot;detail&quot;: &quot;Invalid X-Client-Id or X-Client-Secret Header is not included when payment status is CONFIRMED or FINALIZED.&quot;,
    &quot;cause&quot;: null
}
</code></pre><p>스키마</p><pre><code>{
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>403</td><td><p>예시 값</p><pre><code>{
    &quot;code&quot;: 4030,
    &quot;detail&quot;: &quot;Access denied due to country restrictions.&quot;,
    &quot;cause&quot;: null
}
</code></pre><p>스키마</p><pre><code>{
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>500</td><td><p>예제 값</p><pre><code>{
    &quot;code&quot;: 500,
    &quot;detail&quot;: &quot;Internal server error&quot;,
    &quot;cause&quot;: null
}
</code></pre><p>스키마</p><pre><code>{
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr></tbody></table>

<table data-full-width="false"><thead><tr><th width="230.6944580078125">필드</th><th>제한</th></tr></thead><tbody><tr><td>id</td><td></td></tr><tr><td>구매자 Dapp 포털 주소</td><td>최대 길이 : 42</td></tr><tr><td>pgType</td><td><ul><li>STRIPE</li><li>CRYPTO</li></ul></td></tr><tr><td>상태</td><td><p>결제 상태 &gt;<br></p><ul><li>생성됨</li><li>시작됨</li><li>PG에 등록됨</li><li>캡처됨</li><li>확인됨</li><li>확인 실패</li><li>완료됨</li><li>취소됨</li><li>환불됨</li><li>차지백</li></ul></td></tr><tr><td>통화 코드</td><td><ul><li>USD</li><li>KRW</li><li>JPY</li><li>TWD</li><li>THB</li><li>KAIA</li><li>USDT</li></ul><p>항목의 currencyCode와 동일해야 합니다.</p></td></tr><tr><td>가격</td><td><a href="https://en.wikipedia.org/wiki/ISO_4217">여기에</a> 최소 단위를 입력하세요.<br>예를 들어, 가격이 1달러인 경우 100(센트)를 입력하세요. 각 상품의 가격 합계와<br><br>같아야 합니다. - 소수점 정책<br>STRIPE : 없음<br>CRYPTO : 소수점 이하 4자리까지</td></tr><tr><td>usdExchangeRate</td><td>결제 완료 시점의 환율. pgType이 STRIPE이고 status가 CONFIRMED 또는 FINALIZED인 경우에만 반환됩니다.</td></tr><tr><td>usdExchangePrice</td><td>결제 완료 시 적용된 환율의 USD 가격. pgType이 STRIPE이고 상태가 CONFIRMED 또는 FINALIZED인 경우에만 반환됩니다.</td></tr><tr><td>items(*)</td><td>현재 버전에서는 단일 항목 구매만 지원됩니다.</td></tr><tr><td>testMode</td><td>testMode에 따른 결제 방법은 다음과 같습니다<br><br>. - testMode : false<br>stripe : realmode<br>crypto : kaia<br>- testMode : true<br>stripe : testmode<br>crypto : kairos</td></tr><tr><td>refund</td><td></td></tr><tr><td>refund.type</td><td><ul><li>CHARGEBACK</li><li>REFUND</li></ul></td></tr><tr><td>refund.amount</td><td>가격 정책은 <a href="https://en.wikipedia.org/wiki/ISO_4217">다음과</a> 같습니다. </td></tr><tr><td>refund.chargebackStatus</td><td><ul><li>NEEDS_RESPONSE: 지불 거절이 발생했지만, 이의 제기 또는 이의 신청 전 상태입니다.</li><li>UNDER_REVIEW: 분쟁이 제기되어 현재 STRIPE에서 검토 중입니다.</li><li>승인됨: 분쟁이 승인된 경우.</li><li>LOST: 분쟁 결과가 기각된 경우</li></ul></td></tr></tbody></table>

**응답**

Items(\*)

<table><thead><tr><th width="149.02886962890625">field</th><th>제한</th></tr></thead><tbody><tr><td>itemIdentifier</td><td>최대 길이 : 256</td></tr><tr><td>이름</td><td>최대 길이 : 256</td></tr><tr><td>imageUrl</td><td>최대 길이 : 512</td></tr><tr><td>가격</td><td>예를 들어, 가격이 1달러인 경우 100(센트)를 입력합니다.</td></tr><tr><td>통화 코드</td><td><ul><li>USD</li><li>KRW</li><li>JPY</li><li>TWD</li><li>THB</li><li>KAIA</li><li>USDT</li></ul></td></tr></tbody></table>

**요청 예시**

```bash
curl --location &#x27;https://payment.dappportal.io/api/payment-v1/payment/info?id={payment_id}&#x27; \
--header &#x27;X-Client-Id: {your_client_id}&#x27; \
--header &#x27;X-Client-Secret: {your_client_secret}&#x27;
```

### 3. 결제 상태 조회

 <mark style="background-color:blue;">**</mark>

get

 <mark style="background-color:blue;">**</mark>

   **/api/payment-v1/payment/status**\
\
**매개변수**

| 이름                                                                                 | 설명 |
| ------------------------------------------------------------------------------------ | ----------- |
|<p>id <mark style="color:red;">*필수</mark></p><p>문자열<br><em>(쿼리)</em></p>

| 결제 ID  |

**응답**

<table><thead><tr><th width="145.7642822265625">HTTP 상태 코드</th><th>설명</th></tr></thead><tbody><tr><td>200</td><td><p>예제 값</p><pre class="language-javascript"><code class="lang-javascript">{
    &quot;status&quot;: &quot;{status}&quot;
}
</code></pre><p>스키마</p><pre class="language-javascript"><code class="lang-javascript">{
    status*: String (Enum:[CREATED, STARTED, REGISTERED_ON_PG, CAPTURED, CONFIRMED_FAILED,FINALIZED,CANCELED]
}
</code></pre></td></tr><tr><td>403</td><td><p>예제 값</p><pre class="language-javascript"><code class="lang-javascript">{
    &quot;code&quot;: 4030,
    &quot;detail&quot;: &quot;Access denied due to country restrictions.&quot;,
    &quot;cause&quot;: null
}
</code></pre><p>스키마</p><pre class="language-javascript"><code class="lang-javascript">{
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>404</td><td><p>예제 값</p><pre class="language-javascript"><code class="lang-javascript">{
    &quot;code&quot;: 1002,
    &quot;detail&quot;: &quot;Not found payment&quot;,
    &quot;cause&quot;: null
}
</code></pre><p>스키마</p><pre class="language-javascript"><code class="lang-javascript">{
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>500</td><td><p>예시 값</p><pre class="language-javascript"><code class="lang-javascript">{
    &quot;code&quot;: 500,
    &quot;detail&quot;: &quot;Internal server error&quot;,
    &quot;cause&quot;: null
}
</code></pre><p>스키마</p><pre class="language-javascript"><code class="lang-javascript">{
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr></tbody></table>

<table data-full-width="false"><thead><tr><th>필드</th><th>제한</th></tr></thead><tbody><tr><td>상태</td><td><p>결제 상태 &gt;</p><ul><li>생성됨</li><li>시작됨</li><li>PG에 등록됨</li><li>캡처됨</li><li>확인됨</li><li>확인 실패</li><li>완료됨</li><li>취소됨</li><li>환불됨</li><li>차지백</li></ul></td></tr></tbody></table>

**요청 예시**

```bash
curl --location &#x27;https://payment.dappportal.io/api/payment-v1/payment/status?id={payment_id}&#x27;
```

### 4. 결제 완료

결제 완료 API를 요청한 후 정산 준비가 완료됩니다.

결제 완료 API를 요청하지 않은 경우 STRIPE 거래에 대한 정산을 받을 수 없습니다.\
\
CRYPTO의 경우에도 결제 완료 API 요청을 권장합니다.\
\
**매개변수** \
\
해당 없음

**요청

<table><thead><tr><th>예제 값</th><th>스키마</th></tr></thead><tbody><tr><td><p></p><pre class="language-javascript"><code class="lang-javascript">{
    id: &quot;{payment_id}&quot; 
}
</code></pre></td><td><p></p><pre class="language-javascript"><code class="lang-javascript">{
    id*: String
}
</code></pre></td></tr></tbody></table>

<table><thead><tr><th width="159.82525634765625">HTTP 상태 코드</th><th>설명</th></tr></thead><tbody><tr><td>200</td><td>해당 없음</td></tr><tr><td>403</td><td><p>예시 값</p><pre class="language-javascript"><code class="lang-javascript">{
    &quot;code&quot;: 1004,
    &quot;detail&quot;: &quot;Invalid payment status.&quot;,//Current payment status cannot complete payment finalization
    &quot;cause&quot;: null
}
</code></pre><p>스키마</p><pre class="language-javascript"><code class="lang-javascript">{    
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>403</td><td><p>예시 값</p><pre class="language-javascript"><code class="lang-javascript">{
    &quot;code&quot;: 4030,
    &quot;detail&quot;: &quot;Access denied due to country restrictions.&quot;,
    &quot;cause&quot;: null
}
</code></pre><p>스키마</p><pre class="language-javascript"><code class="lang-javascript">{    
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>404</td><td><p>예제 값</p><pre class="language-javascript"><code class="lang-javascript">{
    &quot;code&quot;: 1002,
    &quot;detail&quot;: &quot;Not found payment&quot;,
    &quot;cause&quot;: null
}
</code></pre><p>스키마</p><pre class="language-javascript"><code class="lang-javascript">{    
    code*: number,
    detail*: String,
    cause: String
}
</code></pre></td></tr><tr><td>500</td><td><p>예시 값</p><pre class="language-javascript"><code class="lang-javascript">{
    &quot;code&quot;: 500,
    &quot;detail&quot;: &quot;Internal server error&quot;,
    &quot;cause&quot;: null
}
</code></pre><p>스키마</p><pre class="language-javascript"><code class="lang-javascript">{    
    code*: number,
    detail*: String,
    cause: String

</code></pre></td></tr></tbody></table>

본문****응답**

**요청 예시**

```bash
curl --location &#x27;https://payment.dappportal.io/api/payment-v1/payment/finalize
--header &#x27;Content-Type: application/json&#x27; \
  --data &#x27;{
    &quot;id&quot;: &quot;{payment_id}&quot;
  }
```

## 03. PaymentProvider

### sdk.getPaymentProvider()

`paymentProvider`를 초기화하여 개발자가 다양한 결제 기능을 사용할 수 있게 합니다.

```javascript
const walletProvider = sdk.getWalletProvider();
```

#### 매개변수

해당 없음

#### 응답

```
PaymentProvider
```

### paymentProvider.startPayment()

`paymentProvider.startPayment()`를 호출하면 사용자에게 거래 창이 표시되고 결제 프로세스가 시작됩니다.

#### 매개변수

payment\_id <mark style="color:red;">\*필수</mark>

· <mark style="color:green;">문자열</mark>

#### 응답

```javascript
Promise<unknown>
```

####

<table><thead><tr><th>코드</th><th>설명</th></tr></thead><tbody><tr><td>-31001</td><td><p><strong>STRIPE</strong> 결제가 취소될 때 이 오류가 발생합니다.</p><pre class="language-json"><code class="lang-json">{
code: -31001,
message:&#x27;Payment is canceled by user or timeout&#x27;
}
</code></pre></td></tr><tr><td>-31002</td><td><pre class="language-json"><code class="lang-json">{
code: -31002,
message:&#x27;Payment is failed&#x27;
}
</code></pre></td></tr><tr><td>-32001</td><td><p>이 오류는 <strong>CRYPTO</strong> 결제가 취소될 때 발생합니다.</p><pre class="language-json"><code class="lang-json">{
code: -32001,
message:&#x27;User denied transaction send.&#x27;
}
</code></pre></td></tr></tbody></table>
오류### paymentProvider.openPaymentHistory()

이 메서드는 결제 내역 창을 엽니다. 작업을 완료하려면 사용자의 서명이 필요합니다.

#### 매개변수

해당 없음

#### 응답

```
Promise<void>
```

## 04. 결제 웹훅

각 웹훅의 콜백 URL은 별도로 설정해야 합니다.

`lockUrl` 및 `unlockUrl`이 필요하지 않은 경우 `null`을 입력하십시오.

### 1. 잠금 이벤트

`lockUrl`은 구매 중인 상품을 일시적으로 잠그거나 예약하기 위해 호출되는 서버 엔드포인트입니다. 이는 일반적으로 **한정 수량** 상품이나 **NFT**의 경우, 초과 판매를 방지하고 현재 결제 진행 중일 때 다른 사용자가 해당 상품을 구매하지 못하도록 하기 위해 필요합니다.

결제 생성 요청에 `lockUrl` 매개변수가 포함된 경우, 잠금 웹훅 이벤트에 대한 POST 메서드 요청이 수행됩니다.

SDK의 startPayment 함수를 사용하여 결제가 시작될 때, 결제가 정상적으로 진행될 수 있다고 판단되면 사용자의 결제 흐름을 시작하기 직전에 웹훅 이벤트가 요청됩니다.

`lockUrl`이 포함된 요청이 이루어졌으나 200 응답을 받지 못한 경우, 결제는 즉시 취소되고 자동으로 실패로 표시됩니다.

```
{
    &quot;paymentId&quot;: &quot;{payment_id}&quot;,
    &quot;itemIdentifiers&quot;: [
        {
            &quot;{your_item_identifier}&quot;
        }
    ]
}
```

### 2. 잠금 해제 이벤트

`unlockUrl`은 **결제가 실패하거나 취소되거나 시간 초과될 때** 호출되는 서버 엔드포인트로, 이전에 잠겨 있던 아이템을 해제하여 다른 사용자가 다시 구매할 수 있도록 합니다.

**결제 생성 요청**에 `unlockUrl` 매개변수가 포함된 경우, 결제 실패 관련 이벤트가 발생하면 이 엔드포인트로 `POST` 요청이 전송됩니다.

결제가 성공적으로 완료된 경우(`status === CONFIRMED`), `unlockUrl`은 **호출되지 않습니다**.
대신 해당 항목은 일반적으로 별도의 프로세스(`finalize` API 또는 내부 로직)를 통해 **최종 확정**됩니다.



 `unlockUrl`이 포함된 요청이 전송되었으나 200 응답을 받지 못한 경우, 1초, 2초, 4초, 8초 간격으로 최대 5회까지 재시도됩니다. 아이템이 잠긴 상태로 유지되는 것을 방지하려면, 잠금 해제를 다시 시도하는 백그라운드 작업을 구현하는 것이 권장됩니다.

```
{
    &quot;paymentId&quot;: &quot;{payment_id}&quot;,
    &quot;itemIdentifiers&quot;: [
        {
            &quot;{your_item_identifier}&quot;
        }
    ]
}
```

### 3. 결제 상태 변경 이벤트

결제 요청 생성 시, 제공한 `paymentStatusChangeCallbackUrl`로 결제 상태 변경 웹훅 이벤트가 전송됩니다.

결제 상태가 **CREATED** 상태인 경우를 제외하고, 결제 상태가 변경될 때마다 이벤트가 발생합니다.

수신된 웹훅의 상태가 **CONFIRMED**인 경우, 결제 완료 API를 호출할 수 있습니다.

paymentStatusChangeCallbackUrl 요청이 200 응답을 받지 못할 경우, 1초, 2초, 4초, 8초 간격으로 최대 5회 재시도됩니다. 5회 재시도 후에도 200 응답을 받지 못하더라도 결제 취소는 진행되지 않습니다.

```
{
    &quot;paymentId&quot;: &quot;{payment_id}&quot;
    &quot;status&quot;: &quot;STARTED|REGISTERED_ON_PG|CAPTURED_CONFIRMED_CONFIRM_FAILED|FINALIZED|CANCELED|REFUNDED|CHARGEBACK&quot;
    &quot;cryptoPaymentInfo&quot;: { // &quot;status&quot;가 CONFIRMED일 때 추가됨
        &quot;paymentTxHash&quot;: &quot;0x..&quot;
        }
}
```

<table data-full-width="false"><thead><tr><th width="527">상태</th><th>설명</th></tr></thead><tbody><tr><td>생성됨</td><td>SDK의 호스트 생성 결제 API는 생성되었지만 호스트 시작 결제는 생성되지 않음</td></tr><tr><td>STARTED</td><td>호스팅된 startPayment는 시작되었으나 사용자의 결제 승인 대기 중 (STRIPE/CRYPTO)</td></tr><tr><td>결제게이트웨이등록</td><td>(pgType = CRYPTO인 경우에만 해당)<br>거래는 승인되었지만, 체인 재구성을 방지하기 위해 충분한 블록 확인을 기다립니다.<br>- 사용자의 KAIA 요청 후 최소 10개의 블록 확인이 필요합니다.</td></tr><tr><td>캡처됨</td><td>(pgType = CRYPTO인 경우에만 해당) 사용자 거래 요청 후 10개<br>블록이 확인된 후 거래 유효성 확인 중</td></tr><tr><td>CONFIRMED</td><td>결제 승인이 완료되었으며 Mini Dapp의 결제 최종 완료를 기다립니다.</td></tr><tr><td>CONFIRM_FAILED</td><td>(pgTye = CRYPTO인 경우에만 해당) 사용자의 거래 요청이 10개의 블록에서<br>확인된 후 거래의 유효성 확인에 실패했습니다.</td></tr><tr><td>FINALIZED</td><td>Mini<br>Dapp의 결제 승인 및 결제 완료로 결제 프로세스가 완료되었습니다. pgType이 CRYPTO인 경우, 최종 결제 API가 호스팅되지 않으면 CONFIRMED 상태에 도달한 후 5분이 지나면 거래가 자동으로 완료됩니다.</td></tr><tr><td>CANCELED</td><td>결제 취소 정책에 따라 결제가 취소되었습니다.</td></tr><tr><td>환불됨</td><td>결제가 환불되었습니다.</td></tr><tr><td>CHARGEBACK</td><td><p>사용자가 직접 지불 거절을 청구했습니다. </p><p>이 웹훅 메시지는 지불 취소(CHARGEBACK) 발생을 포함하여 프로세스의 각 단계에서 전송됩니다.</p></td></tr></tbody></table>
(\*) 이 상태는 결제 정보 조회 API를 통해서만 확인할 수 있습니다.</void></unknown></payment_id>
