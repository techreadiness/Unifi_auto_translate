# Unifi Migration Guide

## Wallet Function Updates

#### Effective Date: To be notified individually

Dear Developers,

This notice is to inform you that Dapp Portal will be rebranded as Unifi.

Along with the rebranding, the Wallet functionality will be updated and certain actions are required to ensure your Apps continue operating smoothly.

#### Concept of Unifi Rebranding

<table><thead><tr><th width="166.141357421875">AS-IS</th><th width="166.203857421875">TO-BE</th><th>NOTE</th></tr></thead><tbody><tr><td>Dapp Portal</td><td>Unifi</td><td></td></tr><tr><td>Mini Dapp</td><td>Unifi Apps</td><td></td></tr><tr><td>Mini Dapp SDK</td><td>Unifi Apps SDK</td><td>No change in the SDK Library name<br>(~/@linenext/dapp-portal-sdk)</td></tr><tr><td>Dapp Portal Wallet</td><td>Unifi Wallet</td><td></td></tr></tbody></table>

## Overview of Unifi

Unifi is a stablecoin wallet built on the Kaia blockchain.

After user registration and Approve authorization, it provides an automatic deposit service.

* Auto-deposit target at launch: USDT
* Other assets (e.g., KAIA, BORA) remain supported but are not eligible for auto-deposit.

Once a Dapp Portal user migrates to Unifi:

* The user's on-chain USDT balance may appear as zero
* All USDT will be automatically deposited into Unifi's account pool

Developers must query the Unifi account balance, not only the on-chain balance. Therefore, Developers using USDT must follow the steps below.

## SDK Version Update Required

The new SDK version that supports Unifi is **v1.5.2**. Please update your SDK to this version.

If not updated:

* USDT Payments via PaymentProvider will fail due to insufficient balance
* Auto-deposited USDT will not be detected

Please update to the Unifi-compatible SDK as soon as it becomes available.

#### Note

By using the PaymentProvider, USDT payments can be executed using the balance automatically deposited in the Unifi account simply by updating the SDK version without modification.

Other functionalities guarantee compatibility with the Unifi Apps SDK, so no changes are required.

## Updated USDT Balance Query Method

* AS-IS: Queries on-chain USDT only

`getErc20TokenBalance()`

* TO-BE: Queries on-chain + Unifi deposit balance

`getErc20TokenBalanceWithDepositedBalance()`

## Smart Contract-Based USDT Transfer Changes

For USDT transfers implemented via smart contract including Swap, Developers must include `depositTokenAddress` and `depositAmount` in the `kaia_sendTransaction` request.

Changes are required when the walletType is WEB or LIFF. If the walletType is OKX or BITGET, developers can use the AS-IS parameters.

* AS-IS

```
params = {
typeInt: 48,
from: "0x4b53..dbe6",
to: "contractAddress",
input: "0xabcd...",
value: "0x0"
}
```

* TO-BE

```
params = {
typeInt: 48,
from: "0x4b53..dbe6",
to: "contractAddress",
input: "0xabcd...",
depositTokenAddress: "0xd077...", // USDT contract address
depositAmount: "100", // Amount of USDT to transfer
value: "0x0" // Kaia Amount
}
```

## Modify Connect Button for Unifi

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

{% file src="../.gitbook/assets/Unifi_Symbol_400x400.svg" %}

{% file src="../.gitbook/assets/Unifi_Symbol_400x400.png" %}
