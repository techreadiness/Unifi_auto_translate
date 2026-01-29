---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/unifi-apps-review-guidelines/how-to-build-successful-unifi-apps
---

# How to build successful Unifi Apps

## Featured on Unifi

The more the Unifi Apps meets the following requirements during onboarding, the more likely it will be featured in the Unifi and attract more users. Please be sure to adhere to the requirements while developing the Unifi Apps.

## Requirements

### Provision of services in various environments with Unifi Apps Connect

**Available Version Combinations**

* LINE MINI App & LINE Login LIFF & Web
* LINE MINI App & Web
* LINE Login LIFF & Web
* LINE MINI App or Web (Single Type)

<figure><img src="../.gitbook/assets/스크린샷 2025-02-06 오전 9.50.03.png" alt=""><figcaption><p>Web3.0 PvsZ | Unifi Apps</p></figcaption></figure>

#### LINE version (LINE MINI App or LINE Login LIFF)

The LINE version can be built using the **LIFF SDK**, allowing users to access your Unifi Apps directly through **LINE Messenger without installing or downloading a separate application**.\
Users can also **invite friends and create a wallet using their logged-in LINE account**, enabling a seamless onboarding experience.

To reduce user drop-off when accessing the LINE version, we **strongly recommend avoiding Wallet Connect on the initial screen** and enabling it **only when necessary**.\
However, since wallet integration may be required for features such as **payments or rewards**, the wallet connection entry point should be **clearly visible and easy to access** when needed.

**User Flow :**&#x20;

* LINE MINI App
  * `Access Unifi Apps(LINE MINI App) → Launch Unifi Apps → Wallet Connect(e.g. at payment or reward step)`
* LINE Login LIFF
  * `Access Unifi Apps(LINE Login LIFF) → Consent to Channel → Add Official Account → Launch Unifi Apps → Wallet Connect(e.g. at payment or reward step)`

<figure><img src="../.gitbook/assets/스크린샷 2025-02-11 오후 2.56.51.png" alt=""><figcaption><p>Web3.0 PvsZ | Unifi Apps</p></figcaption></figure>

#### Web version

The Unifi Apps should also be provided as a **Web version** to support users who are **not familiar with LINE Messenger**.\
The Unifi Apps SDK supports web-based integrations, including **wallet connections via various social accounts**, **Kaia Wallet (mobile app and browser extension)**, **OKX Wallet** and **Bitget Wallet**.

For the Web version, **Wallet Connect must be available on the initial screen** to enable account creation.\
Please note that **Wallet Connect does not refer to LINE Login**; it refers specifically to the **wallet integration functionality provided by the Unifi Apps SDK**.

**User Flow :** \
`Access Unifi Apps(Web) → Wallet Connect → Launch Unifi Apps`

<figure><img src="../.gitbook/assets/스크린샷 2025-02-11 오후 3.09.14.png" alt=""><figcaption><p>Web3.0 PvsZ | Unifi Apps</p></figcaption></figure>

### Provision of In-app item store

The **Unifi Apps SDK** provides multiple payment solutions, including **In-App Purchase (IAP)**, **Crypto**, and **Fiat** payments.\
To establish a sustainable revenue model, services are required to provide an **in-app item store** using the appropriate payment methods based on the supported platform version.

#### Payment Method by Platform

The supported payment methods vary depending on the onboarding version:

* **LINE MINI App**
  * Must provide **In-App Purchase (IAP)** as the primary payment method.
  * Crypto and Fiat payments are **not supported** in the LINE MINI App version.
* **LINE Login LIFF & Web**
  * Must provide **Crypto and Fiat payment methods**.
  * Supported payment options include Crypto payments ($KAIA, USDT) and Fiat payments via STRIPE, all provided through the Unifi Apps SDK.

<figure><img src="../.gitbook/assets/스크린샷 2025-02-06 오전 10.23.29.png" alt=""><figcaption><p>Wizzwoods | Unifi Apps, Midnight Survivors | Unifi Apps</p></figcaption></figure>

### Provision of multi-language

Unifi Apps must provide English and Japanese for users as default. Other languages can be optional as your target country. Classification user country can be done in several ways. You can either follow the browser or system language settings set by the user or determine the country based on the accessed IP address, and based on this, you should provide the appropriate language.

<figure><img src="../.gitbook/assets/MiniDapp_Multi.png" alt=""><figcaption><p>Unifi</p></figcaption></figure>

### Provision of Point Reward

Point rewards can enhance user loyalty. These points can be used as currency within the Unifi Apps and ultimately support exchanges with tokens issued by the Unifi Apps, providing a sense of economic benefit. This can lead to explosive growth for the Unifi Apps.

<figure><img src="../.gitbook/assets/스크린샷 2025-02-06 오전 10.43.32.png" alt=""><figcaption><p>Bombie | Unifi Apps, Heroicarena | Unifi Apps, SuperZ | Unifi Apps</p></figcaption></figure>

### Provision of information about connected wallet

It is very important to make users aware of the information about the connected wallet on any screen of your Unifi Apps. Users may enjoy many Unifi Apps and want to connect different wallets for each. By providing intuitive information about which wallet is connected and what the balance is, you can enhance the convenience that leads to payments.

<figure><img src="../.gitbook/assets/Connected_Wallet.png" alt=""><figcaption><p>Elderglade | Unifi Apps</p></figcaption></figure>

* Wallet Type : [getWalletType()](https://docs.dappportal.io/unifi-apps-sdk/wallet-provider#walletprovider.getwallettype)
* Wallet Address : [kaia\_accounts()](https://docs.dappportal.io/unifi-apps-sdk/wallet-provider#walletprovider.request)
  * If it does not have connected wallet, use kaia\_requestAccounts()
* Wallet Balance : [getErc20TokenBalanceWithDepositedBalance()](https://docs.dappportal.io/unifi-apps-sdk/wallet-provider#walletprovider.geterc20tokenbalancewithdepositedbalance)

### Provision of payment status

It is important for users to clearly understand **what stage their payment is currently in**.

When a payment is initiated through the payment creation API, it is processed and completed through communication with the payment gateway (PG).\
If the payment result or item distribution status is not clearly shown on the screen, users may become unsure whether their payment was successfully completed.

To avoid confusion, the following UI flow should be provided:

* **During the payment process**, display a UI that clearly indicates the payment is being processed (e.g. “Payment in progress”).
* **After receiving the payment completion webhook**, display the item distribution process on the screen.
* Once item distribution is complete, clearly inform the user that the process has finished.

Users should be able to easily follow the full flow on the screen:\
**Payment in progress → Payment completed → Item delivered**

<figure><img src="../.gitbook/assets/PaymentProcess.png" alt=""><figcaption><p>Elderglade | Unifi Apps</p></figcaption></figure>

* [create payment API >](https://docs.dappportal.io/unifi-apps-sdk/payment-provider#id-1.-triggering-createpayment-api-from-mini-dapp)
* [payment status >](https://docs.dappportal.io/unifi-apps-sdk/payment-provider#id-3.-payment-status-change-event)&#x20;

### Guide for Unifi Apps based on Landscape Mode

If your Unifi Apps is optimized for landscape mode, please ensure that it operates in landscape mode even when the user's device is set to portrait mode. It should also function in landscape mode when the auto-rotate feature is used.

<figure><img src="../.gitbook/assets/MiniDapp_Portrait.png" alt=""><figcaption><p>Snake Online | Unifi Apps</p></figcaption></figure>

### Add To Home Screen

<figure><img src="../.gitbook/assets/AddToHome.png" alt=""><figcaption><p>Add to Home Screen | Unifi</p></figcaption></figure>

The Unifi provides users with a shortcut to easily access the Unifi Apps on their mobile home screen.

"Add to Home Screen" feature is provided in two ways:

1. Available on the Unifi Apps detail screen within the Unifi.
2. **Provided by the Unifi Apps (the shortcut URL is provided by the Unifi, and the Unifi Apps will develop a UI to integrate this URL).**
   1. Shortcut URL : https://www.dappportal.io/shortcut.html?dappId=`dappId`\&register=1&\&openExternalBrowser=1\
      \*`dappId`: please find it on your bridge page urls or contact support channel if you don't have.\
      \*register=1: required.\
      \*openExternalBrowser=1: If opening urls from LINE Login LIFF, it allow ot open in external browser.

<figure><img src="../.gitbook/assets/MiniDapp_ATH.png" alt=""><figcaption><p>Add to Home Screen provided by Unifi Apps</p></figcaption></figure>

### Provision of Maintenance Mode

<figure><img src="../.gitbook/assets/스크린샷 2025-05-20 오후 12.59.40.png" alt="" width="224"><figcaption><p>Maintenance Mode | Sample</p></figcaption></figure>

Please provide a maintenance screen during scheduled or emergency maintenance of the Unifi Apps to enhance user experience. In the absence of any notification during maintenance or inaccessibility, it may cause confusion among users.\
It would be helpful to include **the estimated end time and contact information for detailed updates** on the maintenance screen.<br>

### Provision of Close Confirmation Dialog

If a user accidentally presses the back button while playing a Unifi Apps, the current progress may not be saved and the Unifi Apps could be closed unexpectedly. Displaying a confirmation popup when the page is about to be closed is recommended.

<p align="center"><img src="../.gitbook/assets/66 (4).jpg" alt=""><br></p>

You can display a confirmation popup using the following code:

#### Example (React)

Insert the following code in your landing page or layout component:

```javascript

useEffect(() => {
    const preventGoBack = () => {
        if(window.location.pathname === '/') {
            const isConfirmed = confirm('Are you sure you want to go back?');
            if (!isConfirmed) {
                history.pushState(null, '', window.location.pathname)
            }
        }
    };

    window.addEventListener('popstate', preventGoBack);

    // Remove listener when unmounted
    return () => {
        window.removeEventListener('popstate', preventGoBack);
    };
}, []);

```

#### Example (Vanilla JS - `index.html`)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Back Button Blocker</title>
</head>
<body>
  <h1>Home</h1>

  <script>
    if (window.location.pathname === '/') {
      history.pushState(null, '', window.location.pathname);
    }

    function preventGoBack(event) {
      if (window.location.pathname === '/') {
        const isConfirmed = confirm('Are you sure you want to go back?');
        if (!isConfirmed) {
          history.pushState(null, '', window.location.pathname);
        }
      }
    }

    window.addEventListener('popstate', preventGoBack);

    window.addEventListener('beforeunload', () => {
      window.removeEventListener('popstate', preventGoBack);
    });
  </script>
</body>
</html>
```
