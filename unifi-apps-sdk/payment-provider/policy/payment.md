# Payment

## 1️⃣ Supported Payment Methods

<figure><img src="../../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

* <mark style="color:red;">**Unifi Apps must provide both fiat and crypto payment options on the product purchase screen, with each payment button offered separately.**</mark>

### **A. Payment Support Overview**

| Version         | Payment                         | Region     |
| --------------- | ------------------------------- | ---------- |
| LINE MINI App   | IAP Payments                    | Japan Only |
| LINE Login LIFF | Crypto & Stripe (Fiat) payments | Global     |
| Web             | Crypto & Stripe (Fiat) payments | Global     |

### **B. Fiat Payments via IAP (**_**Coming Soon**_**)**

> _In-app billing through LINE App Platform_

### **C. Fiat Payments via Stripe**

> _Global payment processing handled by Stripe_

#### Supported Payment Methods

* Credit / Debit Cards (VISA, Mastercard, AMEX, JCB, etc.)
* Apple Pay
* Google Pay
* Naver Pay (KRW only)
* Kakao Pay (KRW only)

#### Payment Method Rules

* Payment methods automatically adjust depending on:
  * The device OS (iOS / Android)
  * The selected payment currency (USD / Local currencies)
* Available methods may change based on Stripe policies

### D. Crypto Payments

#### Supported cryptocurrencies

* **KAIA**
* **USDT**

## 2️⃣ Supported Currencies & Minimum Charge Limits

<table><thead><tr><th>Type</th><th width="146">Currency</th><th width="139">Decimal(Max)</th><th>Charge(Max)</th><th>Charge(Min)</th></tr></thead><tbody><tr><td>Fiat</td><td>USD</td><td>2</td><td>999,999</td><td>0.50</td></tr><tr><td></td><td>KRW</td><td>0</td><td>999,999</td><td>750</td></tr><tr><td></td><td>JPY</td><td>0</td><td>999,999</td><td>80</td></tr><tr><td></td><td>TWD(NTD)</td><td>2</td><td>999,999</td><td>17</td></tr><tr><td></td><td>THB</td><td>2</td><td>999,999</td><td>18</td></tr><tr><td>Crypto</td><td>KAIA</td><td>4</td><td>999,999</td><td>0.01</td></tr><tr><td></td><td>USDT</td><td>2</td><td>999,999</td><td>0.01</td></tr></tbody></table>

📌 Optional Local Currencies\
Unifi Apps may optionally support additional local currencies depending on the user's region:

* **JPY, TWD, THB, KRW**

📌 Default Pricing Currency

* **USD must be used as the primary pricing reference**

## 3️⃣ Price Display Requirements

All product prices in Unifi Apps **must** be displayed to users in:

* A fiat currency
* A cryptocurrency (KAIA or USDT)

📌 Purpose of dual price presentation

* Provide a **stable purchasing experience**
* Prevent confusion from crypto **price volatility**

## 4️⃣ Payment Request Rules (Developer Input Requirements)

| When user selects       | Merchant must input price as             |
| ----------------------- | ---------------------------------------- |
| Fiat Payment via Stripe | A **fixed** USD-based amount             |
| Crypto Payment          | A **fixed** amount based on KAIA or USDT |

📌 The currency conversion between USD and KAIA/USDT must be implemented and provided by the Unifi Apps.

## 5️⃣ User Notification Requirements

Unifi Apps must provide **clear and real-time** feedback to users about payment status.

Notifications must be:

* **Immediate**
* **Clear**
* **Intuitive**
* Prevent confusion such as double payments or uncertainty about success

<table><thead><tr><th width="167">Event</th><th>Description</th><th>Information to notify users (Example)</th></tr></thead><tbody><tr><td>Successful purchase</td><td>Fiat/Crypto payment successful and item delivered</td><td>Successful purchase</td></tr><tr><td>Purchase failed/canceled</td><td>User requested to process Fiat/Crypto payment but payment failed</td><td>Purchase failed</td></tr><tr><td></td><td>User clicked the "Back" button on the Fiat/Crypto payment screen or exited the screen</td><td>Purchase canceled</td></tr><tr><td></td><td>User clicks the Decline Signature button on the Crypto payment screen</td><td>Purchase canceled</td></tr><tr><td></td><td>User's Crypto balance is insufficient</td><td>Insufficient balance</td></tr><tr><td></td><td>Other errors</td><td>Please try again later</td></tr></tbody></table>

## 6️⃣ Payment History

Unifi Apps must provide a UI that allows users to check their **payment history**.\
Refer to [**Unifi Apps SDK documentation**](https://docs.dappportal.io/unifi-apps-sdk/payment-provider#id-6.-you-can-open-payment-history-page-via-paymentprovider.-promise-will-be-completed-if-payment-histo) for integration methods.

<figure><img src="../../../.gitbook/assets/minimum (3).png" alt=""><figcaption></figcaption></figure>
