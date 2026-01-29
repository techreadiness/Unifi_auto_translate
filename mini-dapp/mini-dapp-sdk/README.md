# Mini Dapp SDK

## Authorization

Mini Dapp must get `clientId` and `clientSecret` to integrate Mini Dapp SDK. This credentials can be activated once service domain has been registered to `clientId`.

## Create Project

To officially open the Mini Dapp, registration of a service domain is mandatory. Be sure to request registration after getting service domain.

If a service domain for the application has not been built, you can use the local environment path for testing. Please use `http://localhost:3000`.&#x20;

To use the paymentProvider, a `clientSecret` is required. **DO NOT share `clientSecret` to public.** If it has been exposed, please request to issue a new `clientSecret`.&#x20;

## Install SDK

Add Mini Dapp SDK into your project via npm or yarn.

```
npm install @linenext/dapp-portal-sdk
```

or

```
yarn add @linenext/dapp-portal-sdk
```

## Initiate SDK&#x20;

<mark style="color:red;">**Mini Dapp MUST call DappPortalSDK.Init() when the user executes Mini Dapp. In case of LIFF version, the must be done after liff.init() is completed.**</mark>&#x20;

At this stage, you only need to implement up to `DappPortalSDK.Init()` and completing the Mini Dapp Connect is **not** required at this stage.  \
Mini Dapp Connect(Wallet Integration) within the LIFF environment should only be triggered **when necessary** (e.g., to receive on-chain rewards, make item purchases), not upon initial LIFF entry.)

* Background : This approach is necessary to handle data for active user verification in the Mini Dapp. This data is crucial for performance measurement and developing user acquisition strategies.
* Notice : Following this guide will provide LINE NEXT with the encrypted information of LINE users connected to the Mini Dapp.

## class DappPortalSDK

#### 1. DappPortalSDK(config: DappPortalSDKClientConfig)

* Initialize SDK using clientId.
* The previously provided clientId is used. The SDK only runs on the pre-agreed Host address.

#### DappPortalSDKClientConfig

* clientId: string
* chainId: string
* SDK is running on production env basically. If you want to connect testnet, use _‘1001’_.

#### 2. getWalletProvider(): WalletProvider

* You can get WalletProvider which is compatible with EIP-1193 interface.

#### 3. getPaymentProvider() : PaymentProvider

* You can get PaymentProvider which support process and history of payment.

#### 4. isSupportedBrowser(): boolean

* It is function to verify compatibility between SDK and Browser.

#### 5. showUnsupportedBrowserGuide(): Promise

* It will show a screen how to use an external browser if current browser is not supported.
