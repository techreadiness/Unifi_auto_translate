# 가스 수수료 위임

## 카이아 웨이브 빌더를 위한 카이아 수수료 위임 프로그램

### 1. 소개

카이아 네트워크의 수수료 위임은 다른 계정이 거래 가스 수수료를 지불할 수 있도록 하는 기능입니다. 이를 통해 사용자는 거래 가스 수수료로 자신의 $KAIA를 지출하지 않고도 거래를 수행할 수 있습니다.

[신청서 &gt;](https://docs.google.com/forms/d/e/1FAIpQLScSMnI8fD1xbyeoAL3TI81YxT3V1UfoByca84M7TZzYII5Pmw/viewform)

### 2. 개념

#### 1. 카이아 수수료 위임은 세 가지 주요 구성 요소로 이루어집니다:

1. 발신자: 거래를 제출하는 계정 (from)
2. Dapp: 사용자가 서명한 거래를 수수료 지불자 서버로 중계하는 중계자
3. 수수료 지불자 서버: 수수료 지불자로 서명하고 서명된 거래를 네트워크로 전송하며 영수증을 호출자에게 반환

#### 2. 카이아 수수료 위임의 운영 절차는 다음과 같습니다:

1. 발신자가 거래를 생성합니다.
2. 송신자는 거래 내 수수료 지불자의 주소를 지정합니다.
3. 송신자는 거래에 서명합니다.
4. 송신자는 서명된 거래를 Dapp 백엔드로 전송합니다.
5. 백엔드는 수수료 지불 서버에 거래 서명을 요청합니다.
6. 수수료 지불 서버는 수수료 지불자로서 거래에 서명하고, 네트워크로 전송한 후 거래 영수증을 획득하여 거래 영수증을 반환합니다.

### 3. 코드 샘플

#### 1. 필수 조건

1. SDK
   1. kaia-sdk의 일부인 ethers-ext가 설치되어 있어야 합니다.
   2. ethers-ext [시작하기](https://docs.kaia.io/ko/references/sdk/ethers-ext/getting-started/)
2. 지갑
   1. 수수료 위임은 다음 지갑에서만 지원됩니다.
      1. [kaia-wallet](https://www.kaiawallet.io/) 모바일/확장 프로그램, [dapp-portal-wallet](https://wallet.dappportal.io/) liff/웹
   2. dapp 프론트엔드는 지갑을 통해 사용자가 서명한 거래를 가져와야 합니다.

#### 2. 웹 애플리케이션 코드 스니펫

**프론트엔드 (React) - 사용자 서명 트랜잭션 획득**

`수수료 위임된 가치 전송 예시`

```
import { Web3Provider } from &quot;@kaiachain/ethers-ext&quot;;
import { TxType, parseKaia } from &quot;@kaiachain/js-ext-core&quot;;
import DappPortalSDK from &quot;@linenext/dapp-portal-sdk&quot;;
import { useEffect, useState } from &quot;react&quot;;

// 테스트넷
const feePayer = &quot;0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266&quot;;
// 메인넷
const feePayer = &quot;0x22a4ebd6c88882f7c5907ec5a2ee269fecb5ed7a&quot;;

const clientId = &quot;30e…b89&quot;;
const chainId = &quot;1001&quot;;

export default function home() {
 const [provider, setProvider] = useState<any>(null);
 const [accounts, setAccounts] = useState<string[]>
 ([]);

 const initProvider = async () =&gt; {
   const sdk = await DappPortalSDK.init({
     clientId,
     chainId,
   });
   const provider = new Web3Provider(sdk.getWalletProvider());
   const accounts = await provider.send(&quot;kaia_requestAccounts&quot;, []);
   setProvider(provider);
   setAccounts(accounts);
 };

 const sign = async () =&gt; {
   const tx = {
     typeInt: TxType.FeeDelegatedValueTransfer,
     from: accounts[0],
     to: accounts[0],
     value: parseKaia(&quot;0.1&quot;).toHexString(),
     feePayer,
   };
   const signedTx = await provider.send(&quot;kaia_signTransaction&quot;, [tx]);

   // 서명된 트랜잭션을 백엔드로 전송
   console.log(signedTx);
 };

 useEffect(() =&gt; {
   initProvider();
 }, []);

 return (
   <div>
     <button onClick={sign}>사용자 서명된 트랜잭션 가져오기</button>
   </div>
 );
}
```

`수수료 위임형 스마트 계약 실행 예시`

```
import { Web3Provider } from &quot;@kaiachain/ethers-ext&quot;;
import { TxType, parseKaia } from &quot;@kaiachain/js-ext-core&quot;;
import DappPortalSDK from &quot;@linenext/dapp-portal-sdk&quot;;
import { useEffect, useState } from &quot;react&quot;;

const feePayer = &quot;0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266&quot;;
const clientId = &quot;30e…b89&quot;;
const chainId = &quot;1001&quot;;
const contractAddr = &quot;0x95Be48607498109030592C08aDC9577c7C2dD505&quot;;
const abi = &#x27;[...]&#x27; //https://docs.kaia.io/ko/references/sdk/ethers-ext/v6/smart-contract/write/에서 복사

export default function home() {
const [provider, setProvider] = useState<any>(null);
const [accounts, setAccounts] = useState<string[]>
([]);

const initProvider = async () =&gt; {
  const sdk = await DappPortalSDK.init({
    clientId,
    chainId,
  });
  const provider = new Web3Provider(sdk.getWalletProvider());
  const accounts = await provider.send(&quot;kaia_requestAccounts&quot;, []);
  setProvider(provider);
  setAccounts(accounts);
};

const sign = async () =&gt; {
  const contract = new ethers.Contract(contractAddr, abi, provider);
  const contractCallData = await contract.increment.populateTransaction();
  const tx = {
    typeInt: TxType.FeeDelegatedSmartContractExecution, // 수수료 위임형 스마트 계약 실행
    from: accountAddress,
    to: contractCallData.to,
    input: contractCallData.data,
    value: &quot;0x0&quot;,
    feePayer: feePayer,
  };
  const signedTx = await provider.send(&quot;kaia_signTransaction&quot;, [tx]);
  // 서명된 트랜잭션을 백엔드로 전송
  console.log(signedTx);
};

useEffect(() =&gt; {
  initProvider();
}, []);

return (
  <div>
    <button onClick={sign}>사용자 서명된 트랜잭션 가져오기</button>
  </div>
);
}
```

**백엔드 - feePayer 서버에 &#x27;sign&#x27; 요청**

1. 입력 : userSignedTx - RLP 인코딩된 트랜잭션
2. 반환 : 트랜잭션 영수증
3. feePayer 서버 URL
   1. [https://fee-delegation.kaia.io](https://fee-delegation.kaia.io) (메인넷)
      1. 계약 또는 발신자는 등록되어야 함
   2. [https://fee-delegation-kairos.kaia.io](https://fee-delegation-kairos.kaia.io/) (테스트넷)

```
const { Wallet } = require(&quot;@kaiachain/ethers-ext/v6&quot;);
const ethers = require(&quot;ethers&quot;);

//테스트넷
const feePayerServer = &quot;https://fee-delegation-kairos.kaia.io&quot;;
const provider = new ethers.JsonRpcProvider(&quot;https://public-en-kairos.node.kaia.io&quot;);

async function main() {
/* 프론트엔드 측에서 사용자가 서명한 트랜잭션 */
const signedTxRLPEncoded = {
   raw: RLP 인코딩된 서명된 TX 16진수 문자열
}
const response = await fetch(`${feePayerServer}/api/signAsFeePayer`, {
  method: &quot;POST&quot;,
  headers: {
    &quot;Content-Type&quot;: &quot;application/json&quot;,
  },
  body: JSON.stringify({ userSignedTx:signedTxRLPEncoded }),
});
const data = await response.json();
console.log(data);
}

main();
```

4. 잔액 확인

```
const checkBalance = async () =&gt; {
 // 수수료 위임을 위해 등록한 계약 또는 발신자의 주소입니다
 const address = &quot;0x63d4f17d2a8a729fd050f7679d961b1dfbb1e3af&quot;;
 const result = await fetch(`${feePayerServer}/api/balance?address=${address}`);
 const isEnough = (await result.json()).data;
 console.log(isEnough ? &quot;잔액 충분&quot; : &quot;잔액 부족&quot;);
};
```</string[]></any></string[]></any>
