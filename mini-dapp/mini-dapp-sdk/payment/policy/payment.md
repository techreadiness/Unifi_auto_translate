# Payment

## Payment Methods

<figure><img src="../../../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

* <mark style="color:red;">**Mini Dapps must provide both fiat and crypto payment options on the product purchase screen, with each payment button offered separately.**</mark>

### a. Fiat

Payment methods support credit/debit cards (major brands such as VISA, MasterCard, AMEX, JCB, etc.), Apple Pay, Google Play, Naver Pay (KRW only), and Kakao Pay (KRW only).

* Payment methods dynamically and automatically change depending on the OS and payment currency of the connected device.
* Payment method may change in the future depending on the payment processor's policy.
* LINE IAP payment will be available soon.

Fiat payments are supported in both the LIFF and Web versions of Mini Dapp.

### b. Crypto

KAIA and USDT are supported as a payment method.

Crypto payments are supported in both the LIFF and Web versions of Mini Dapp.

## Supported Currencies

<table><thead><tr><th>Type</th><th width="146">Currency</th><th width="139">Decimal(Max)</th><th>Charge(Max)</th><th>Charge(Min)</th></tr></thead><tbody><tr><td>Fiat</td><td>USD</td><td>2</td><td>999,999</td><td>0.50</td></tr><tr><td></td><td>KRW</td><td>0</td><td>999,999</td><td>750</td></tr><tr><td></td><td>JPY</td><td>0</td><td>999,999</td><td>80</td></tr><tr><td></td><td>TWD(NTD)</td><td>2</td><td>999,999</td><td>17</td></tr><tr><td></td><td>THB</td><td>2</td><td>999,999</td><td>18</td></tr><tr><td>Crypto</td><td>KAIA</td><td>4</td><td>999,999</td><td>0.01</td></tr><tr><td></td><td>USDT</td><td>2</td><td>999,999</td><td>0.01</td></tr></tbody></table>

## Product Price

* **The prices of products sold through the Mini Dapp SDK must be presented to users in both fiat currency and cryptocurrency with a certain level of stability.**
  * This aims to provide a stable purchasing experience for both Web2 and Web3 users, prevent confusion caused by excessive price fluctuations, and balance the needs of Web2 and Web3 users. By doing so, it seeks to create a purchasing environment that is understandable, trustworthy, and reliable for all users.
* USD is the default payment currency.
* Each Mini Dapp may optionally support additional local currencies (JPY, TWD, THB, KRW) based on user's country information of needed.

| User County (based on browser language) | Product price currencies shown to users                                        |
| --------------------------------------- | ------------------------------------------------------------------------------ |
| Japan                                   | <ul><li>Default : USD, KAIA, USDT</li><li>Optional : JPY, KAIA, USDT</li></ul> |
| Thailand                                | <ul><li>Default : USD, KAIA, USDT</li><li>Optional : THB, KAIA, USDT</li></ul> |
| Taiwan                                  | <ul><li>Default : USD, KAIA, USDT</li><li>Optional : TWD, KAIA, USDT</li></ul> |
| South Korea                             | <ul><li>Default : USD, KAIA, USDT</li><li>Optional : KRW, KAIA, USDT</li></ul> |
| Others                                  | <ul><li>Default : USD, KAIA, USDT</li></ul>                                    |

### Product price to enter when requesting payment

* When a user selects Fiat payment, Mini Dapp operator must enter a fixed amount based USD to request payment.
* When a user selects Crypto payment, Mini Dapp operator must enter a fixed amount based on $KAIA to request payment.

### Provide Clear Notifications

* <mark style="color:red;">**To minimize errors such as duplicate payments or incorrect payments, the Dapp must provide appropriate notification messages to the user immediately so that the user can recognize the results of successful and failed/canceled purchases in a "clear" and "intuitive" manner**</mark>

<table><thead><tr><th width="167">Event</th><th>Description</th><th>Information to notify users (Example)</th></tr></thead><tbody><tr><td>Successful purchase</td><td>Fiat/Crypto payment successful and item delivered</td><td>Successful purchase</td></tr><tr><td>Purchase failed/canceled</td><td>User requested to process Fiat/Crypto payment but payment failed</td><td>Purchase failed</td></tr><tr><td></td><td>User clicked the "Back" button on the Fiat/Crypto payment screen or exited the screen</td><td>Purchase canceled</td></tr><tr><td></td><td>User clicks the Decline Signature button on the Crypto payment screen</td><td>Purchase canceled</td></tr><tr><td></td><td>User's Crypto balance is insufficient</td><td>Insufficient balance</td></tr><tr><td></td><td>Other errors</td><td>Please try again later</td></tr></tbody></table>

### Payment History

**Refer to SDK document and provide payment history to the user in the appropriate location.**

<figure><img src="../../../../.gitbook/assets/minimum (3).png" alt=""><figcaption></figcaption></figure>
