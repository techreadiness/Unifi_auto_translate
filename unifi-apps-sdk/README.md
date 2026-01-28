---
hidden: true
---

# Unifi Apps SDK

## 1. Getting Started

### Latest Version

* npm: [https://www.npmjs.com/package/@linenext/dapp-portal-sdk/v/1.5.2](https://www.npmjs.com/package/@linenext/dapp-portal-sdk/v/1.5.2)
* cdn: [https://static.kaiawallet.io/js/dapp-portal-sdk-1.5.2.js](https://static.kaiawallet.io/js/dapp-portal-sdk-1.5.2.js)

### How to get SDK Access(clientId & clientSecret)

To integrate Unifi Apps SDK, you need to receive a `clientId` and `clientSecret` from the Unifi team.

**Steps:**

1. [Submit the SDK Terms & Conditions form](https://docs.dappportal.io/join-us#mini-dapp-sdk), including your Unifi Apps information.
2. Receive your `clientId` and `clientSecret` via the submitted email.

⚠️ **Never expose `clientSecret` publicly.** If it has been compromised, request regeneration via Tech Support.

### Project Setup & Domain Registration

* Your `clientId` becomes active only when a domain is registered.
  * For testing purposes, you may use `http://localhost:3000`.&#x20;
  * For external test domains, please request whitelisting via Tech Support or email.
* Payments via `paymentProvider` require a valid `clientSecret`.

### Install SDK

Install the SDK via npm, yarn, or pnpm

```
npm install @linenext/dapp-portal-sdk
# or
yarn add @linenext/dapp-portal-sdk
# or
pnpm add @linenext/dapp-portal-sdk
```

## 2. SDK Initialization

### Initialize the SDK

You **must initialize the SDK** each time the Unifi Apps is loaded.

```javascript
import DappPortalSDK from '@linenext/dapp-portal-sdk'

const sdk = await DappPortalSDK.init({
  clientId: '<CLIENT_ID>',
  chainId: '1001', // or '8217' for mainnet
});
```

**Parameters**

| Name                                                                       | Description                                                                                                       |
| -------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| <p>clientId<mark style="color:$danger;">*required</mark> </p><p>string</p> | the clientId provided when applying for the SDK                                                                   |
| <p>chainId </p><p>string</p>                                               | The default value is **1001**(testnet). To use the mainnet after development, set the value to **8217**(mainnet). |

**Response**

Returns a `DappPortalSDK` object through which the following methods can be called.

```
DappPortalSDK
```

### **⚠️ LINE MINI App and LINE Login LIFF version note**

* Call `liff.init()` **before** calling `DappPortalSDK.init()`.
* Do **not** trigger wallet connection(`connectWallet`) on LINE MINI App or LINE Login LIFF entry. Only connect when needed(e.g., item purchase, on-chain rewards).
* This ensures accurate tracking of active users and attribution via LINE.

### 💡 **Best Practice**

* **Initialize the SDK only once** and manage the `DappPortalSDK` instance as a **singleton**.
* Avoid calling `DappPortalSDK.init()` multiple times—it may cause **unexpected behavior or malfunctions**.

We **do not enforce** singleton usage by default to allow **multi-configuration setups**(e.g., using both **testnet** and **mainnet** in a single app).\
In such cases, manage **one singleton instance per configuration**(e.g., one for testnet, one for mainnet).

## 3. SDK API Reference

### **DappPortalSDK Class**

#### **Constructor**

`DappPortalSDK(config: DappPortalSDKClientConfig)`

Initializes the SDK using your credentials.

* `clientId: string` (Provided by the Unifi team)
* `chainId: string` ("1001" for testnet, "8217" for mainnet)

#### **Instance Methods**

**`getWalletProvider(): WalletProvider`**

Returns EIP-1193-compatible wallet provider instance.

* This allows you to send transactions, sign messages, and interact with wallets.

**`getPaymentProvider(): PaymentProvider`**

Returns the object for managing payments and transaction history.

**`isSupportedBrowser(): boolean`**

Checks if the current browser is compatible.

**`showUnsupportedBrowserGuide(): Promise<void>`**

Displays a guide prompting the user to open in a supported browser.

## 4. Security Guidelines

* Keep `clientSecret` confidential.
* Never commit it to source control.
* If exposed, rotate it immediately via Tech Support.
