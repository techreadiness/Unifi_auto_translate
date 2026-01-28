# Gas Fee Delegation

## Kaia Fee Delegation Program for Kaia Wave Builders

### 1. Introduction

The fee delegation of kaia network is a feature that allows another account to pay for the transaction gas fee. This allows users to perform transactions without spending their own $KAIA for the gas fee of a transaction.

[Apply Form >](https://docs.google.com/forms/d/e/1FAIpQLScSMnI8fD1xbyeoAL3TI81YxT3V1UfoByca84M7TZzYII5Pmw/viewform)

### 2. Concept

#### 1. kaia fee delegation consist of three main compenents:

1. Sender: The account submitting the transaction (from)
2. Dapp: The relayer that relay the user signed transaction to the fee payer server
3. Fee payer server: Sign as fee payer and send the signed transaction to the network and return the receipt to the caller

#### 2. The operations of kaia fee delegation is as follows:

1. The sender creates the transaction.
2. The sender specifies the fee payer's address in the transaction.
3. The sender signs the transaction.
4. The sender sends the signed transaction to backend of dapp.
5. The backend requests a transaction sign to the fee payer server.
6. The fee payer server signs the transaction as a fee payer, sends it to the network, gets a receipt of the transaction and returns the transaction receipt.

### 3. Code Samples

#### 1. Prequisite

1. SDK
   1. ethers-ext that is one of kaia-sdk should be installed.
   2. ethers-ext [getting-started](https://docs.kaia.io/ko/references/sdk/ethers-ext/getting-started/)
2. Wallet
   1. fee-delegation is only supported by
      1. [kaia-wallet](https://www.kaiawallet.io/) mobile/extension, [dapp-portal-wallet](https://wallet.dappportal.io/) liff/web
   2. dapp frontend should get a user signed transaction via the wallets

#### 2. code snippet in web application

**frontend (React) - getting a user signed transaction**

`fee-delegated value transfer example`

```
import { Web3Provider } from "@kaiachain/ethers-ext";
import { TxType, parseKaia } from "@kaiachain/js-ext-core";
import DappPortalSDK from "@linenext/dapp-portal-sdk";
import { useEffect, useState } from "react";

// testnet
const feePayer = "0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266";
// mainnet
const feePayer = "0x22a4ebd6c88882f7c5907ec5a2ee269fecb5ed7a";

const clientId = "30e…b89";
const chainId = "1001";

export default function home() {
 const [provider, setProvider] = useState<any>(null);
 const [accounts, setAccounts] = useState<string[]>([]);

 const initProvider = async () => {
   const sdk = await DappPortalSDK.init({
     clientId,
     chainId,
   });
   const provider = new Web3Provider(sdk.getWalletProvider());
   const accounts = await provider.send("kaia_requestAccounts", []);
   setProvider(provider);
   setAccounts(accounts);
 };

 const sign = async () => {
   const tx = {
     typeInt: TxType.FeeDelegatedValueTransfer,
     from: accounts[0],
     to: accounts[0],
     value: parseKaia("0.1").toHexString(),
     feePayer,
   };
   const signedTx = await provider.send("kaia_signTransaction", [tx]);

   // send the signed tx to backend
   console.log(signedTx);
 };

 useEffect(() => {
   initProvider();
 }, []);

 return (
   <div>
     <button onClick={sign}>Get user signed tx</button>
   </div>
 );
}
```

`fee-delegated smart contract execution example`

```
import { Web3Provider } from "@kaiachain/ethers-ext";
import { TxType, parseKaia } from "@kaiachain/js-ext-core";
import DappPortalSDK from "@linenext/dapp-portal-sdk";
import { useEffect, useState } from "react";

const feePayer = "0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266";
const clientId = "30e…b89";
const chainId = "1001";
const contractAddr = "0x95Be48607498109030592C08aDC9577c7C2dD505";
const abi = '[...]' //copy from https://docs.kaia.io/ko/references/sdk/ethers-ext/v6/smart-contract/write/

export default function home() {
const [provider, setProvider] = useState<any>(null);
const [accounts, setAccounts] = useState<string[]>([]);

const initProvider = async () => {
  const sdk = await DappPortalSDK.init({
    clientId,
    chainId,
  });
  const provider = new Web3Provider(sdk.getWalletProvider());
  const accounts = await provider.send("kaia_requestAccounts", []);
  setProvider(provider);
  setAccounts(accounts);
};

const sign = async () => {
  const contract = new ethers.Contract(contractAddr, abi, provider);
  const contractCallData = await contract.increment.populateTransaction();
  const tx = {
    typeInt: TxType.FeeDelegatedSmartContractExecution, // fee delegated smart contract execution
    from: accountAddress,
    to: contractCallData.to,
    input: contractCallData.data,
    value: "0x0",
    feePayer: feePayer,
  };
  const signedTx = await provider.send("kaia_signTransaction", [tx]);
  // send the signed tx to backend
  console.log(signedTx);
};

useEffect(() => {
  initProvider();
}, []);

return (
  <div>
    <button onClick={sign}>Get user signed tx</button>
  </div>
);
}
```

**backend - request 'sign' to feePayer server**

1. input : userSignedTx - RLP encoded transaction
2. return : transaction receipt
3. feePayer server URL
   1. [https://fee-delegation.kaia.io](https://fee-delegation.kaia.io) (mainnet)
      1. Contract or sender should be registered
   2. [https://fee-delegation-kairos.kaia.io](https://fee-delegation-kairos.kaia.io/) (testnet)

```
const { Wallet } = require("@kaiachain/ethers-ext/v6");
const ethers = require("ethers");

//testnet
const feePayerServer = "https://fee-delegation-kairos.kaia.io";
const provider = new ethers.JsonRpcProvider("https://public-en-kairos.node.kaia.io");

async function main() {
/* signed tx from user on frontend side */
const signedTxRLPEncoded = {
   raw: RLP encoded signed TX hex string
}
const response = await fetch(`${feePayerServer}/api/signAsFeePayer`, {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({ userSignedTx:signedTxRLPEncoded }),
});
const data = await response.json();
console.log(data);
}

main();
```

4. balance check

```
const checkBalance = async () => {
 // It's an address of contracts or senders you registered for fee delegation
 const address = "0x63d4f17d2a8a729fd050f7679d961b1dfbb1e3af";
 const result = await fetch(`${feePayerServer}/api/balance?address=${address}`);
 const isEnough = (await result.json()).data;
 console.log(isEnough ? "enough balance" : "not enough balance");
};
```

