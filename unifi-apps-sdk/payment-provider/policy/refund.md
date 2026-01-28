# Refund

<mark style="color:red;">**Unifi Apps should establish and communicate a clear and fair non-refund policy to users, considering the following principles.**</mark>

## 1️⃣ Global Non-Refund Policy

* **Refunds, exchanges, returns, and cancellations are not allowed** for digital products such as game items.
* All user inquiries and disputes regarding transactions between Unifi Apps and users must be handled **directly by the Unifi Apps operator**.
* **LINE NEXT does not intervene**, mediate, or provide support for refund disputes.

## 2️⃣ Fiat Payments

| Item           | Policy                                                 |
| -------------- | ------------------------------------------------------ |
| Refunds        | Not permitted                                          |
| Reason         | Digital product are considered consumed once delivered |
| Responsibility | Unifi Apps must manage all user disputes independently |

## 3️⃣ Crypto Payments

| Item             | Policy                                                 |
| ---------------- | ------------------------------------------------------ |
| Refunds          | Not permitted                                          |
| Price Volatility | Not a valid reason for refund                          |
| Responsibility   | Unifi Apps must manage all user disputes independently |

## **4️⃣ Mandatory UX Requirements**

Unifi Apps must **clearly** inform users of the non-refund policy **before** payment.

### Minimum Required

| Display Location                           | Required Text                                                                                                                                                    |
| ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Directly below the Purchase/Payment button | <ul><li>You agree that the product(s) is/are non-refundable.</li><li>If paid via LINE IAP, you agree to providing encrypted ID info to LY Corporation.</li></ul> |

### Recommended Implementation

| Requirement  | Description                                                    |
| ------------ | -------------------------------------------------------------- |
| Checkbox     | Users must check to acknowledge **non-refund policy**          |
| Action Block | Purchase button must remain disabled until checkbox is checked |
| View Details | Provide full refund policy and data usage details              |

If you choose to implement the **View Details** option, please ensure that the following information is included.

| Infomation                          | Requirement                                                                                              |
| ----------------------------------- | -------------------------------------------------------------------------------------------------------- |
| Receiving Party                     | LY Corporation                                                                                           |
| Purpose for Provision               | Processing product payments                                                                              |
| Personal Information to be provided | Encrypted Identification Information                                                                     |
| Retention Period of Receiving Party | Until the purpose of provision is achieved                                                               |
| Country of Incorporation            | Japan                                                                                                    |
| Company URL                         | [https://www.lycorp.co.jp/](https://www.lycorp.co.jp/)                                                   |
| Company Privacy Policy              | [https://www.lycorp.co.jp/en/company/privacypolicy/](https://www.lycorp.co.jp/en/company/privacypolicy/) |

<figure><img src="../../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>
