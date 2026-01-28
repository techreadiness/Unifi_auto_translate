# FAQ

## SDK Issuance & Environment Setup

<details>

<summary>Q. When will the SDK be issued?</summary>

A. The SDK will be issued within **3 business days** from the date of submitting the SDK T\&C. \
The `clientId` and `clientSecret` will be sent to your registered email.

</details>

<details>

<summary>Q. Do we need to develop both Web and LINE(LIFF) versions?</summary>

A. Yes, that’s correct.\
The LINE(LIFF) version is designed for LINE users and allows seamless access within the LINE mobile app.\
On the other hand, the Web version is accessible via mobile browsers or PC environments, and it's intended for non-LINE users who do not use LINE Login.

</details>

<details>

<summary>Q. Do we need to configure <code>chainId</code> for the SDK?</summary>

A. Yes. The `chainId` is used to distinguish between the testnet and mainnet environments.\
By default, it is set to testnet(`chainId: 1001`).\
During development, please use the testnet to test wallet integration and payment flows.\
For real payment testing or official launch, you must switch to the mainnet(`chainId: 8217`).

</details>

<details>

<summary>Q. Where can I get updates about SDK version changes?</summary>

A. SDK version updates are announced through the official Telegram channel.\
📢 [Join the official Telegram channel](https://t.me/+Fq6bbac7NLhmNGJl)\
Once you join, you’ll receive the latest updates and announcements related to the SDK.

</details>

<details>

<summary>Q. Can I integrate the Mini Dapp SDK with Unity or Cocos engine?</summary>

A. Yes, you can.\
By porting your Unity or Cocos project to WebGL, you can integrate it as a web application using the Mini Dapp SDK.\
For detailed instructions, please refer to the integration guide.

</details>

<details>

<summary>Q. Do you provide sample code?</summary>

A. Sample code is provided in the following document.

* Sample code by method: [https://minidapp-demo.dappportal.io/](https://minidapp-demo.dappportal.io/method)
* Full integration sample code: [https://docs.dappportal.io/mini-dapp/overview/dapp-starter](https://docs.dappportal.io/mini-dapp/overview/dapp-starter)

</details>

## Wallet Provider

<details>

<summary>Q. Why does an “Invalid Origin” error occur and wallet connection fail?</summary>

A. The SDK only works properly on domains registered in the whitelist.\
Please share your test domain via the Tech Support Channel or email, and we will assist you in registering it to the domain whitelist.

</details>

<details>

<summary>Q. Why is the wallet connection window not opening?</summary>

A. If `DappPortalSDK.init()` is repeatedly called on every request in the Web/LIFF version, it may cause malfunction. Therefore, we strongly recommend calling `DappPortalSDK.init()` only once during app startup and managing it as a singleton instance.\
In addition, for the LIFF version, make sure to call `DappPortalSDK.init()` **after** `liff.init()` has been successfully completed.

</details>

<details>

<summary>Q. Why does OKX Wallet fail to connect or require re-entry to the Mini Dapp on certain devices when using <code>kaia_requestAccounts</code> and <code>personal_sign</code>?</summary>

A. This issue is typically caused by timing conflicts during the signature step after wallet connection. To ensure a more stable experience, we recommend using `kaia_connectAndSign` instead.

</details>

<details>

<summary>Q. How can I persist the Wallet Connect session when re-entering or refreshing the Mini Dapp after wallet connection?</summary>

A. First, call `kaia_accounts` to check if there is an existing connected wallet.

* If a connected wallet is found, you can use that wallet information directly.
* If no connected wallet is found, proceed with wallet reconnection using `kaia_requestAccounts` or `kaia_connectAndSign`.

</details>

<details>

<summary>Q. Why is it necessary to implement <code>disconnectWallet()</code>?</summary>

A. You need to implement `disconnectWallet()` in the following cases:

* When the user has lost the password for the previously connected wallet,
* When the wallet connected via [wallet.dappportal.io](https://wallet.dappportal.io) differs from the one connected in the Mini Dapp,
* Or when the user wants to switch to a different wallet.

In such cases, access to the Mini Dapp may be restricted. Implementing `disconnectWallet()` allows users to disconnect the current wallet and connect a new one.

</details>

<details>

<summary>Q. Can I provide external wallets such as MetaMask instead of using the Mini Dapp SDK wallet integration?</summary>

A. No, it is not allowed. \
To launch a Mini Dapp, you must use the wallet integration method provided by the Mini Dapp SDK. External wallet integrations such as MetaMask are not supported.

</details>

<details>

<summary>Q. How are user accounts identified?</summary>

A. In both Web and LINE(LIFF) versions, user accounts should be distinguished by their wallet address.\
However, in the LINE version, users can enter the Mini Dapp without connecting a wallet.\
In such cases, you should temporarily create an account based on the user's LINE ID upon first entry, and map the Wallet Address to that account once the wallet connection is completed.

</details>

<details>

<summary>Q. Should accounts be compatible between Web and LINE(LIFF) versions?</summary>

A. Yes.\
Both Web and LINE(LIFF) versions support wallet types such as LINE, OKX, and Bitget Wallet.\
If the same wallet address is used in both environments, it is recommended to maintain compatibility between the accounts for a seamless user experience and consistent login and asset information.

</details>

<details>

<summary>Q. Can I retrieve LINE ID or profile info via LINE Login in the Web version?</summary>

A. No, the Web version does not support LINE Login. If implemented, it must be removed.\
The Web version is intended for non-LINE users, including PC users, and should not include features that require LINE authentication.\
LINE-related features should be provided only in the LIFF version.

</details>

<details>

<summary>Q. Is there a way to distinguish between LIFF and Web browser environments?</summary>

A. Yes. You can use the `liff.isInClient()` method to detect the environment.

* If `liff.isInClient()` returns `true`: This indicates the LIFF environment. In this case, run `liff.init()` first, then call `DappPortalSDK.init()`.
* If `liff.isInClient()` returns `false`: This indicates a standard web environment. Only call `DappPortalSDK.init()`.

</details>

<details>

<summary>Q. Why is Bitget Wallet not shown in the wallet selection list?</summary>

A. To display Bitget Wallet in the wallet list, you must register a `projectId`.\
Please follow the [guide documentation](https://docs.dappportal.io/mini-dapp/mini-dapp-sdk/wallet/domain-verification-via-reown) to create a `projectId`, then submit it through the Tech Support channel for registration.

</details>

<details>

<summary>Q. What causes unknown errors when signing a transaction with a connected wallet?</summary>

A. This may occur if the Wallet Address requesting the signature differs from the actual signing Wallet Address.\
Please check that the Wallet Address connected via:

* Web: [https://wallet.dappportal.io/](https://wallet.dappportal.io/)
* LIFF: [https://liff.line.me/2006533014-r4jJyjy2](https://liff.line.me/2006533014-r4jJyjy2)

is the same Wallet Address being used for signing.

</details>

## Payment Provider

<details>

<summary>Q. Do we need to support both Crypto and Stripe payments?</summary>

A. Yes, both payment methods must be supported.\
However, if adjustments are required due to specific service structures or policies, you may selectively support one method after consultation with the BD or Tech Support channel.

</details>

<details>

<summary>Q. Why does an error occur during payment testing?</summary>

A. Please first check whether the parameters you provided match the [example request code](https://docs.dappportal.io/mini-dapp/mini-dapp-sdk/payment#id-1.-triggering-createpayment-api-from-mini-dapp) in the documentation.\
Even if the code seems correct, errors may still occur during testing.\
If the issue persists, please contact the Tech Support channel for assistance.

</details>

<details>

<summary>Q. What are <code>lockUrl</code> and <code>unlockUrl</code>?</summary>

A. These are useful features when selling products with limited stock.\
They temporarily “lock” the quantity while a user is attempting to purchase the product, preventing other users from buying the same item simultaneously.\
This mechanism helps avoid duplicate purchases during the payment process and enables more accurate inventory management.

⚠️ Note: If the product has **no quantity limit**, set both `lockUrl` and `unlockUrl` to `null`.

</details>

<details>

<summary>Q. <strong>Crypto payment works, but why does Stripe payment fail?</strong> (An error code 500 is returned when <code>startPayment()</code> is called)</summary>

A. This usually happens when the `imageUrl` parameter is invalid or not accessible from outside.\
Please make sure the product image URL is valid and publicly accessible.

</details>

<details>

<summary>Q. Why isn’t the webhook being received?</summary>

A. The `paymentStatusChangeCallbackUrl` must be accessible over the public network.\
You should either:

* Make the URL publicly accessible, or
* Whitelist the Dapp Portal server IPs.

Additionally, the callback **must return an HTTP 200 OK response** to ensure successful webhook delivery.

</details>

<details>

<summary>Q. Why does <code>createPayment</code> succeed but <code>startPayment</code> return an error? (An error code 400 is returned when <code>startPayment()</code> is called)</summary>

A. This indicates that something went wrong during the `startPayment` phase.\
Please check the `paymentId` and the returned error code used in the test.\
For root cause analysis and further assistance, share the details via the Tech Support channel.

</details>

<details>

<summary>Q. What causes an "Internal JSON-RPC error" or a blank payment screen to appear?</summary>

A. This issue typically occurs when the configured `chainId` and `testMode` values do not match.

* **Testnet:** `chainId: 1001`, `testMode: true`
* **Mainnet:** `chainId: 8217`, `testMode: false`

Please ensure that these values are correctly configured according to the environment and try testing again.

</details>

<details>

<summary>Q. How can I perform real payment testing?</summary>

A. Real payment testing is only available **after your settlement information has been updated**.\
This update is completed **after your team submits the Due Diligence (DD) form**.

Once your launch schedule is confirmed, the Kaia Wave team will request your DD submission.\
In general, real payment testing becomes available **three business days before the official launch**.

If you need to test earlier, please contact the Tech Support channel to request an exception.

⚠️ Note: Real payment tests **are non-refundable**, so please proceed with caution.

</details>

<details>

<summary>Q. Is there a minimum payment amount for products?</summary>

A. Yes, there is a minimum payment threshold:

* **USD**: Minimum of **$0.5**
* **KAIA**: Minimum of **0.01 KAIA**

For more details, please refer to the [guide documentation](https://docs.dappportal.io/mini-dapp/mini-dapp-sdk/payment/policy/payment#supported-currencies).

</details>

<details>

<summary>Q. Is it mandatory to apply exchange rates for Crypto payment products?</summary>

A. Yes, you **must provide a converted price based on the current market rate**.\
This ensures transparency for users and accuracy in payment processing.

While the SDK **does not provide exchange rate conversion**, you can use external services such as:

* CoinMarketCap(CMC)
* Kaiascan Open API

to fetch real-time price data and apply it accordingly.

</details>

<details>

<summary>Q. Why is it necessary to provide a payment history feature?</summary>

A. Users must be able to view their own payment history, which:

* Increases user trust
* Helps customer support(CS) by referencing `paymentId` and other data

The SDK provides an `openPaymentHistory()` function, so please implement this in:

* The **In-App Store page**, or
* Any other screen that users frequently visit.

</details>

## LINE Integration

<details>

<summary>Q. How do I create a LINE Developers account?</summary>

A. Developers must use their **personal LINE account** to create a **LINE Business ID (Provider)**.

* Shared or team accounts are **not supported** in Dapp Portal.

If you're unable to create the account, please contact the **Tech Support channel** for assistance.

</details>

<details>

<summary>Q. What should I do if I can't create a LINE MINI App?</summary>

A. Mini Dapp **do not support LINE MINI App**.\
Instead, use a combination of the **LINE Login channel** and **Messaging API channel** to build your LIFF version.

Please build your LIFF app based on the **LINE Login channel**, not LINE MINI App.

</details>

<details>

<summary>Q. How should I set the "Region to provide the service" when creating a LINE Login channel?</summary>

A. This setting should reflect the **primary target country of your service**, **not the country where your company is incorporated**.

Regardless of the selected region:

* All LINE-available countries can access your service
* There are **no functional differences** based on the selected region

</details>

<details>

<summary>Q. How do I link an OA (Official Account) to a LINE Login channel?</summary>

A. Follow these steps:

1. Create the OA: Under the same Provider, create a Messaging API channel and generate an OA.
2. Enable Messaging API:\
   Go to [https://manager.line.biz/account](https://manager.line.biz/account) → Settings → Enable Messaging API → Select Provider → Agree
3. Link the OA:\
   LINE Login Channel → Basic Settings → Add Friend Option → Linked LINE Official Account → Select OA

</details>

<details>

<summary>Q. How do I create a LIFF URL?</summary>

A. Follow these steps:&#x20;

LINE Login Channel → LIFF → Add → Fill in LIFF Details

* LIFF app name: Your dApp service name
* Size: Full
* Endpoint URL: Your service domain
* Scopes: `openid` (required), `profile` (optional), `chat_message.write` (unchecked)
* Add friend option: On (aggressive)
* Module mode: Disabled

</details>

<details>

<summary>Q. How do I enable OA Aggressive Add Friend mode?</summary>

A. Follow these steps:

LINE Login Channel → LIFF → LIFF Detail → Add Friend Option → On (aggressive)

</details>

<details>

<summary>Q. Why am I getting a 403 error when accessing the LINE(LIFF) version?</summary>

A. LIFF URLs are **inaccessible** if the LINE Login channel is not in **Published** status.\
Please switch to **Published** mode when submitting your Demo or performing tests.

</details>

<details>

<summary>Q. Is it okay to publish the LINE(LIFF) version before launch?</summary>

A. Yes. As long as you **do not share the LIFF URL or test domain externally**, general users won’t have access.

Publishing early can help streamline Demo submission and testing.\
If you **must test without publishing**, you can **add the reviewer’s email as an admin** to the LINE Login channel.

</details>

## Web3 Provider

<details>

<summary>Q. What causes the error: “Sending transaction was failed after ~ try, network is busy”?</summary>

A. This is a **temporary error** caused by **high network traffic**.\
If this occurs, simply retry the transaction — it should eventually succeed.

</details>

