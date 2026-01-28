# How to build successful Mini Dapp

## Featured on Dapp Portal

The more the Mini Dapp meets the following requirements during onboarding, the more likely it will be featured in the Dapp Portal and attract more users. Please be sure to adhere to the requirements while developing the Mini Dapp.

## Requirements

### Provision of services in various environments with Mini Dapp Connect

Clients must build Mini Dapp wtih two types of LINE and Web version.&#x20;

<figure><img src="../.gitbook/assets/스크린샷 2025-02-06 오전 9.50.03.png" alt=""><figcaption><p>Web3.0 PvsZ | Mini Dapp</p></figcaption></figure>

#### LINE version

LINE version can be built via LIFF SDK. Users can easily access your Mini Dapp through LINE Messenger without install or download application. Also, Users could invite their friends and create wallet with LINE account logged in.

We strongly recommend providing Wallet Connect only when needed, rather than on the initial screen, to reduce the drop rate of users accessing the LINE version. However, since wallet integration may be essential when offering rewards, it would be advisable to place the wallet integration button where it can be easily found.

User Flow : \
Access Mini Dapp(LIFF) -> Consent Channel -> Add OA -> Play Mini Dapp -> Wallet Connect (at neccessary steop e.g. payment, reward)

<figure><img src="../.gitbook/assets/스크린샷 2025-02-11 오후 2.56.51.png" alt=""><figcaption><p>Web3.0 PvsZ | Mini Dapp</p></figcaption></figure>

#### Web version

Mini Dapp must be build in Web version to users who does not familiar with LINE Messenger. Mini Dapp SDK provides integration of web environment including wallet connection via various social account, Kaia Wallet(Mobile App/Extension) and OKX Wallet.

In the case of the web version, Wallet Connect must be provided on the initial screen for account creation. Wallet Connect does not refer to LINE Login; it refers to wallet integration provided through the Mini Dapp SDK.

User Flow : \
Access Mini Dapp(Web) -> Wallet Connect -> Play Mini Dapp

<figure><img src="../.gitbook/assets/스크린샷 2025-02-11 오후 3.09.14.png" alt=""><figcaption><p>Web3.0 PvsZ | Mini Dapp</p></figcaption></figure>

#### Compatibility between LINE and Web version

The account system of the two versions of the Mini Dapp should operate based on the Wallet Address to ensure account compatibility between the two versions.

When connecting a wallet in the LIFF and Web version, if connection proceeds with Mini Dapp Wallet(LINE) or OKX Wallet, the Wallet Address will be the same across both versions, ensuring account information compatibility.\
However, the Web version's Mini Dapp Wallet(Kaia Wallet App/Extension and Social logins excluding LINE) cannot be compatible with LIFF's.

<figure><img src="../.gitbook/assets/Wallet_Compatibility.png" alt=""><figcaption></figcaption></figure>

_For example, User A has created Mini Dapp Wallet via LINE Account 'a' from Web version, It is same with LIFF's if user logged in LINE Messenger with LINE Account 'a'._

### Provision of In-app item store

Mini Dapp SDK provide payment solution both of Crypto($KAIA) and Fait(STRIPE). To create your revenue model, an in-app item store must be established.

<figure><img src="../.gitbook/assets/스크린샷 2025-02-06 오전 10.23.29.png" alt=""><figcaption><p>Wizzwoods | Mini Dapp, Midnight Survivors | Mini Dapp</p></figcaption></figure>

### Provision of multi-language

Mini Dapp must provide English and Japanese for users as default. Other languages can be optional as your target country. Classification user country can be done in several ways. You can either follow the browser or system language settings set by the user or determine the country based on the accessed IP address, and based on this, you should provide the appropriate language.

<figure><img src="../.gitbook/assets/MiniDapp_Multi.png" alt=""><figcaption><p>Dapp Portal</p></figcaption></figure>

### Provision of Point Reward

Point rewards can enhance user loyalty. These points can be used as currency within the Mini Dapp and ultimately support exchanges with tokens issued by the Mini Dapp, providing a sense of economic benefit. This can lead to explosive growth for the Mini Dapp.

<figure><img src="../.gitbook/assets/스크린샷 2025-02-06 오전 10.43.32.png" alt=""><figcaption><p>Bombie | Mini Dapp, Heroicarena | Mini Dapp, SuperZ | Mini Dapp</p></figcaption></figure>

### Provision of information about connected wallet

It is very important to make users aware of the information about the connected wallet on any screen of your Mini Dapp. Users may enjoy many Mini Dapps and want to connect different wallets for each. By providing intuitive information about which wallet is connected and what the balance is, you can enhance the convenience that leads to payments.

<figure><img src="../.gitbook/assets/Connected_Wallet.png" alt=""><figcaption><p>Elderglade | Mini Dapp</p></figcaption></figure>

* Wallet Type : [getWalletType()](https://docs.dappportal.io/mini-dapp/mini-dapp-sdk/wallet-provider#a.-getwallettype-wallettype-or-null)
* Wallet Address : [kaia\_accounts()](https://docs.dappportal.io/mini-dapp/mini-dapp-sdk/wallet-provider#b.-async-request-requestargs-requestarguments-promise)
  * If it does not have connected wallet, use kaia\_requestAccounts()
* Wallet Balance : [kaia\_getBalance()](https://docs.kaia.io/ko/references/json-rpc/kaia/get-balance/)

### Provision of payment status

It is very important to inform users about the payment progress status. After starting the payment using the payment creation API, the payment is processed and completed through communication with the payment gateway (PG). If the payment completion and item distribution notifications are not appropriately provided on the user's screen, they may not be able to confirm whether the payment was completed. Once the payment starts, a UI that shows the payment status should be provided during the payment process, and upon receiving the payment completion webhook, the process of distributing the items should be displayed on the payment screen.

<figure><img src="../.gitbook/assets/PaymentProcess.png" alt=""><figcaption><p>Elderglade | Mini Dapp</p></figcaption></figure>

* [create payment API >](https://docs.dappportal.io/mini-dapp/mini-dapp-sdk/payment-provider#id-01.-payment)
* [payment status >](https://docs.dappportal.io/mini-dapp/mini-dapp-sdk/payment-provider#id-05.-payment-status)&#x20;

### Guide for Mini Dapp based on Landscape Mode

<figure><img src="../.gitbook/assets/MiniDapp_Portrait.png" alt=""><figcaption><p>Snake Online | Mini Dapp</p></figcaption></figure>

If your Mini Dapp is optimized for landscape mode, please ensure that it operates in landscape mode even when the user's device is set to portrait mode. It should also function in landscape mode when the auto-rotate feature is used.

### Add To Home Screen

<figure><img src="../.gitbook/assets/AddToHome.png" alt=""><figcaption><p>Add to Home Screen | Dapp Portal</p></figcaption></figure>

The Dapp Portal provides users with a shortcut to easily access the Mini Dapp on their mobile home screen.

"Add to Home Screen" feature is provided in two ways:

1. Available on the Mini Dapp detail screen within the Dapp Portal.
2. **Provided by the Mini Dapp (the shortcut URL is provided by the Dapp Portal, and the Mini Dapp will develop a UI to integrate this URL).**
   1. Shortcut URL : https://www.dappportal.io/shortcut.html?dappId=`dappId`\&register=1&\&openExternalBrowser=1\
      \*`dappId`: please find it on your bridge page urls or contact support channel if you don't have.\
      \*register=1: required.\
      \*openExternalBrowser=1: If opening urls from LIFF, it allow ot open in external browser.

<figure><img src="../.gitbook/assets/MiniDapp_ATH.png" alt=""><figcaption><p>Add to Home Screen provided by Mini Dapp</p></figcaption></figure>

### Provision of Maintenance Mode

<figure><img src="../.gitbook/assets/스크린샷 2025-05-20 오후 12.59.40.png" alt="" width="224"><figcaption><p>Maintenance Mode | Sample</p></figcaption></figure>

Please provide a maintenance screen during scheduled or emergency maintenance of the Mini Dapp to enhance user experience. In the absence of any notification during maintenance or inaccessibility, it may cause confusion among users.\
It would be helpful to include **the estimated end time and contact information for detailed updates** on the maintenance screen.<br>

### Provision of Close Confirmation Dialog

If a user accidentally presses the back button while playing a MIni Dapp, the current progress may not be saved and the Mini Dapp could be closed unexpectedly. Displaying a confirmation popup when the page is about to be closed is recommended.

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
