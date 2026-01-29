---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/mini-dapp/mini-dapp-sdk/initiate-dappportalsdk
---

# Initiate DappPortalSDK

## Initiate SDK

#### 1. Initialize SDK via `init()` method&#x20;

```javascript
import DappPortalSDK from '@linenext/dapp-portal-sdk'

const sdk = await DappPortalSDK.init({ clientId: '<CLIENT_ID>', chainId: '1001 });
```

**Parameters**

| Name                                                               | Description                                                                                                                                           |
| ------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>clientId<mark style="color:red;">*required</mark><br>string</p> | the clientId provided when applying for the SDK                                                                                                       |
| <p>chainId<br>string</p>                                           | <p>The default value is <strong>1001</strong>(testnet).<br>To use the mainnet after development, set the value to <strong>8217</strong>(mainnet).</p> |

**Response**\
Returns a `DappPortalSDK` object through which the following methods can be called.

```
DappPortalSDK
```

| method name                                                       | description                                                                     |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| **getWalletProvider**  <mark style="color:blue;">function</mark>  | Initialize walletProvider                                                       |
| **getPaymentProvider** <mark style="color:blue;">function</mark>  | Initialize paymentProvider                                                      |
| **isSupportedBrowser** <mark style="color:blue;">function</mark>  | Returns `true` if the current browser is supported; otherwise, returns `false`. |

<mark style="color:green;">**We highly recommend executing DappPortalSDK.init() only once and managing it as a singleton object. If you create a new DappPortalSDK object by calling DappPortalSDK.init() every time you make a request to the wallet, it may lead to malfunction. The reason we do not enforce this as a singleton is to support scenarios where multi-configurations are needed. For example, if you want to use both testnet and mainnet in a single app. In such cases, we also recommend managing one singleton DappPortalSDK object for testnet and another singleton for mainnet.**</mark>
