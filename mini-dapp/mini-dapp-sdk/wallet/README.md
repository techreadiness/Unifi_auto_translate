---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/mini-dapp/mini-dapp-sdk/wallet
---

# Wallet

The WalletProvider follows the [EIP-1193](https://eips.ethereum.org/EIPS/eip-1193) standard and supports the EventEmitter interface defined in it.

## sdk.getWalletProvider()

Initializes the `walletProvider`, allowing developers to use various wallet features.

```javascript
const walletProvider = sdk.getWalletProvider();
```

**Parameters**\
\
N/A

**Responses**

```javascript
WalletProvider
```

## walletProvider.getWalletType()

Returns the type of the currently connected wallet.

```javascript
const walletType = walletProvider.getWalletType();
```

**Parameters**\
\
N/A\
\
**Responses**

```javascript
enum WalletType {
    Web = "Web",
    Liff = "Liff",
    Extension = "Extension",
    Mobile = "Mobile",
    OKX = "OKX",
    BITGET = "BITGET"
}
```

## walletProvider.request()

This function provides JSON-RPC API format on request. You can send request to retrieve healthy status of chain and sign transaction with wallet. If you send it before wallet connection, user will see a screen to select wallet type to connect.

You can find the available KAIA-related methods, their parameters, and corresponding responses in the table below. RPC methods that are not included in the table will be requested directly to the chain node and please refer to Kaia docs' [RPC API Reference](https://docs.kaia.io/ko/references/).<br>

```javascript
const getAccount = async() => {
   const accounts = await walletProvider.request({ method: 'kaia_accounts' }) as string[]; 
   return accounts[0]; 
} 

const requestAccount = async () => {
   const addresses = await walletProvider.request({ method: 'kaia_requestAccounts' }) as string[];
   return accounts[0];
}

const connectAndSign = async (msg:string) => {
   const [account, signature] = await walletProvider.request({ method: 'kaia_connectAndSign', params: [msg]}) as string[];
   return [account, signature];
}

const getBalance = async(params: [account:string,blockNumberOrHash:'latest' | 'earliest'])=>{
   return await walletProvider.request({ method: 'kaia_getBalance', params: params });
}

const transaction = {
  from: 0xYourWalletAddress, //The currently connected wallet account can be retrieved using the kaia_accounts method.
  to: '0xRecipientAddress', //Please replace it with a valid wallet address.
  value: '0x10',
  gas: '0x5208', //general gas usage for Kaia transaction
};

const sendTransaction = async(transaction) => {
    const transactionHash = await walletProvider.request({ method: 'kaia_sendTransaction', params: [transaction]});
    return transactionHash;
};
```

\
**Parameters**\
\
RequestArguments <mark style="color:red;">\*required</mark> · <mark style="color:green;">object</mark>\
&#x20; \
&#x20; \- method <mark style="color:red;">\*required</mark> · <mark style="color:green;">string</mark>

&#x20; \- params <mark style="color:green;">unknown\[]</mark>\
\
**Responses**

```
Promise<unknown>
```

<table><thead><tr><th width="315.21563720703125">method</th><th width="155.862548828125">params</th><th>Responses</th></tr></thead><tbody><tr><td><p><strong>kaia_accounts</strong><br></p><p>Returns the list of addresses currently connected to the wallet.<br>If no wallet is connected, an empty array is returned.</p></td><td>null</td><td><pre class="language-javascript"><code class="lang-javascript">['Account1']
</code></pre></td></tr><tr><td><strong>kaia_requestAccounts</strong><br><br>Initiates wallet connection.<br>During the process, a window is displayed for the user to select a wallet provider.<br>Returns a list of addresses associated with the selected wallet.</td><td>null</td><td><pre class="language-javascript"><code class="lang-javascript">['Account1']
</code></pre></td></tr><tr><td><p><strong>personal_sign</strong> (<a href="https://eips.ethereum.org/EIPS/eip-191">EIP-191</a>)</p><p><br>Initiate sign procedure. We recommend to use <code>personal_sign</code> to get compatibility with various wallets including OKX Wallet.</p></td><td>[message: <mark style="color:green;">string</mark>, account: <mark style="color:green;">string</mark>]</td><td><pre class="language-javascript"><code class="lang-javascript">"0xa3f20717a250c2b0b729b7e5becbff67fdaef7e0699da4de7ca5895b02a170a12d887fd3b17bfdce3481f10bea41f45ba9f709d39ce8325427b57afcfc994cee1b"
</code></pre><p><sup>signature</sup></p></td></tr><tr><td><strong>kaia_connectAndSign</strong>  (<a href="https://eips.ethereum.org/EIPS/eip-191">EIP-191</a>) <mark style="color:red;"><code>recommended</code></mark> <br><a data-footnote-ref href="#user-content-fn-1"><br></a>Iniitiates wallet connection and signing.<br>Prompts the user to select a wallet provider, then signs the provided message.<br>Returns <code>[account, signature]</code> as an array.</td><td>[message: <mark style="color:green;">string</mark>]</td><td><pre class="language-javascript"><code class="lang-javascript">["account","0xa3f20717a250c2b0b729b7e5becbff67fdaef7e0699da4de7ca5895b02a170a12d887fd3b17bfdce3481f10bea41f45ba9f709d39ce8325427b57afcfc994cee1b"]
</code></pre><p><sup>account and signature as Array</sup></p></td></tr><tr><td><strong>kaia_getBalance</strong><br><br>Returns the kaia balance. </td><td><p>[account: <mark style="color:green;">string</mark>, blockNumberOrHash: <mark style="color:green;">string</mark>]<br><br><sup>blockNumberOrHash can be set as <code>latest</code> or <code>earliest</code></sup><br></p><ul><li><sup><code>latest</code>: the most recent block</sup> </li><li><sup><code>earliest</code>: the genesis block (block 0)</sup></li></ul></td><td><p><br><br></p><pre class="language-javascript"><code class="lang-javascript">"0x00000000000000000"
</code></pre><p><sup>the balance value in</sup> <a href="https://docs.kaia.io/learn/token-economics/kaia-native-token/#units-of-kaia-"><sup>kei</sup></a><sup>, the smallest unit of the KAIA blockchain.</sup> <br><sup>1 KAIA = 10^18 kei</sup></p></td></tr><tr><td><strong>kaia_sendTransaction</strong><br><br>Constructs a transaction with given parameters<br></td><td>[{<br>    from: <mark style="color:green;">string</mark>,<br>    to: <mark style="color:green;">string</mark>,<br>    value: <mark style="color:green;">string</mark>,<br>    gas: <mark style="color:green;">string</mark> <br>}]<br><br><sup><code>from</code> field should be the account that achieved from 'kaia_accounts'<strong>,</strong>'kaia_requestAccounts' or 'kaia_connectAndSign'</sup></td><td><p></p><pre class="language-javascript"><code class="lang-javascript">"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d059210"26d1527331
</code></pre><p><sup>transactionHash</sup></p></td></tr></tbody></table>

#### Error

```
{code: -32001, message: 'User canceled'}
```

<table><thead><tr><th>Code</th><th>Description</th></tr></thead><tbody><tr><td>-32001</td><td><pre class="language-javascript"><code class="lang-javascript">{
  "code": -32001,
  "message": "User canceled" 
}
</code></pre><pre class="language-javascript"><code class="lang-javascript">//When the user dismissed the wallet connection popup.
{code: -32001, message: 'User closed popup', data: null}
</code></pre><pre class="language-javascript"><code class="lang-javascript">//When the user clicks the dismiss button on the signature popup
{
  "code": -32001,
  "message": "User denied message signature"
}
</code></pre><pre class="language-javascript"><code class="lang-javascript">//When the user clicks the dismiss button on the transaction popup
{
  "code": -32001,
  "message": "User denied transaction send."
}
</code></pre></td></tr><tr><td>-32004</td><td>Invalid from address (Please retry methohs after executing <code>walletProvider.disconnectWallet()</code>)</td></tr><tr><td>-32005</td><td>User logged out due to incorrect password input (Please retry methohs after executing <code>walletProvider.disconnectWallet()</code>)</td></tr><tr><td>-32006</td><td>Wallet is not connected yet (If an error occurs while the wallet in connected, Please retry methods after executing <code>walletProvider.disconnectWallet()</code>. If an error occurs while the wallet is not connected, please connect wallet first)</td></tr></tbody></table>

## walletProvider.disconnectWallet()

Disconnects the wallet.\
When this function is called, a confirmation window will appear to confirm the disconnection.

```javascript
 const disconnectWallet = async ()=>{
    await walletProvider.disconnectWallet();
    window.location.reload();
}
```

**Parameters**\
\
N/A\
\
**Responses**\
\
N/A\
<br>

## walletProvider.getErc20TokenBalance()

```javascript
const getErc20TokenBalance = async(contractAddress:string,account:string)=> {
    return await walletProvider.getErc20TokenBalance(contractAddress,account);
}

const USDTContractAddress = '0xd077a400968890eacc75cdc901f0356c943e4fdb';
const account = 'my_account_address';
getErc20TokenBalance(USDTContractAddress, account).then(balance => {
    const formattedUSDTBalance = Number(microUSDTHexToUSDTDecimal(balance as string)).toFixed(2);
    //microUSDTHexToUSDTDecimal is format function to transform hexadecimal string to decimal string
    //https://github.com/techreadiness/dapp-starter/blob/main/src/utils/format.ts
    console.log(formattedUSDTBalance);
    //0.00
})
```

#### Parameters

contactAddress <mark style="color:red;">\*required</mark> · <mark style="color:green;">string</mark>\
account <mark style="color:red;">\*required</mark> · <mark style="color:green;">string</mark>

#### Responses

64-byte hexadecimal string.\
The returned value includes the token’s decimal scaling according to its `decimals` specification.

For example, USDT uses a decimal scale of 10⁶, while DELABS uses a decimal scale of 10¹⁸.

```
string
```

## Compatible Libraries

* [https://docs.kaia.io/ko/references/sdk/ethers-ext/getting-started/](https://docs.kaia.io/ko/references/sdk/ethers-ext/getting-started/)
* [https://docs.kaia.io/ko/references/sdk/web3js-ext/getting-started/](https://docs.kaia.io/ko/references/sdk/web3js-ext/getting-started/)
* [https://docs.kaia.io/ko/references/sdk/caver-js/](https://docs.kaia.io/ko/references/sdk/caver-js/)

[^1]: <sup>ddd</sup>
