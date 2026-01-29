# 지갑

WalletProvider는 [EIP-1193](https://eips.ethereum.org/EIPS/eip-1193) 표준을 따르며, 여기에 정의된 EventEmitter 인터페이스를 지원합니다.

## sdk.getWalletProvider()

`walletProvider`를 초기화하여 개발자가 다양한 지갑 기능을 사용할 수 있게 합니다.

```javascript
const walletProvider = sdk.getWalletProvider();
```

**매개변수**\
\
해당 없음

**반환값**

```javascript
WalletProvider
```

## walletProvider.getWalletType()

현재 연결된 지갑의 유형을 반환합니다.

```javascript
const walletType = walletProvider.getWalletType();
```

**매개변수**\
\
해당 없음\
\
**반환값**

```javascript
enum WalletType {
    Web = &quot;Web&quot;,
    Liff = &quot;Liff&quot;,
    Extension = &quot;Extension&quot;,
    Mobile = &quot;Mobile&quot;,
    OKX = &quot;OKX&quot;,
    BITGET = &quot;BITGET&quot;
}
```

## walletProvider.request()

이 함수는 요청 시 JSON-RPC API 형식을 제공합니다. 체인의 정상 상태를 조회하거나 지갑으로 거래를 서명하는 요청을 보낼 수 있습니다. 지갑 연결 전에 요청을 보내면 사용자에게 연결할 지갑 유형을 선택하는 화면이 표시됩니다.

사용 가능한 KAIA 관련 메서드, 해당 매개변수 및 응답은 아래 표에서 확인할 수 있습니다. 표에 포함되지 않은 RPC 메서드는 체인 노드에 직접 요청되며, Kaia 문서의 [RPC API 참조](https://docs.kaia.io/ko/references/)를 참조하십시오.<br>

```javascript
const getAccount = async() =&gt; {
   const accounts = await walletProvider.request({ method: &#x27;kaia_accounts&#x27; }) as string[]; 
   return accounts[0]; 
} 

const requestAccount = async () =&gt; {
   const addresses = await walletProvider.request({ method: &#x27;kaia_requestAccounts&#x27; }) as string[];
   return accounts[0];
}

const connectAndSign = async (msg:string) =&gt; {
   const [account, signature] = await walletProvider.request({ method: &#x27;kaia_connectAndSign&#x27;, params: [msg]}) as string[];
   return [account, signature];
}

const getBalance = async(params: [account:string,blockNumberOrHash:&#x27;latest&#x27; | &#x27;earliest&#x27;])=&gt;{
   return await walletProvider.request({ method: &#x27;kaia_getBalance&#x27;, params: params });
}

const transaction = {
  from: 0xYourWalletAddress, //현재 연결된 지갑 계정은 kaia_accounts 메서드로 조회 가능
  to: &#x27;0xRecipientAddress&#x27;, //유효한 지갑 주소로 대체해 주세요
  value: &#x27;0x10&#x27;,
  gas: &#x27;0x5208&#x27;, //Kaia 트랜잭션의 일반적인 가스 사용량
};

const sendTransaction = async(transaction) =&gt; {
    const transactionHash = await walletProvider.request({ method: &#x27;kaia_sendTransaction&#x27;, params: [transaction]});
    return transactionHash;
};
```

\
**매개변수**\
\
RequestArguments <mark style="color:red;">\*필수</mark> · <mark style="color:green;">객체</mark>\
  \
  \- method <mark style="color:red;">\*필수</mark> · 문자열

  \- params <mark style="color:green;">알 수 없음\[]</mark>\
\
**반환값**

```
Promise<unknown>
```

<table><thead><tr><th width="315.21563720703125">메소드</th><th width="155.862548828125">매개변수</th><th>응답</th></tr></thead><tbody><tr><td><p><strong>kaia_accounts</strong><br></p><p>지갑에 현재 연결된 주소 목록을 반환합니다. 지갑이<br>연결되어 있지 않으면 빈 배열이 반환됩니다.</p></td><td>null</td><td><pre class="language-javascript"><code class="lang-javascript">[&#x27;Account1&#x27;]
</code></pre></td></tr><tr><td><strong>kaia_requestAccounts</strong> 지갑<br><br>연결을 시작합니다.<br>이 과정에서 사용자가 지갑 공급자를 선택할 수 있는 창이 표시됩니다. 선택한 지갑과<br>연결된 주소 목록을 반환합니다.</td><td>null</td><td><pre class="language-javascript"><code class="lang-javascript">[&#x27;Account1&#x27;]
</code></pre></td></tr><tr><td><p><strong>personal_sign</strong> (<a href="https://eips.ethereum.org/EIPS/eip-191">EIP-191</a>)</p><p><br>서명 절차를 시작합니다. OKX Wallet을 비롯한 다양한 지갑과의 호환성을 확보하기 위해 <code>personal_sign</code> 를 사용하여 OKX Wallet을 포함한 다양한 지갑과의 호환성을 확보할 것을 권장합니다.</p></td><td>[message: <mark style="color:green;">string</mark>, account: <mark style="color:green;">string</mark>]</td><td><pre class="language-javascript"><code class="lang-javascript">&quot;0xa3f20717a250c2b0b729b7e5becbff67fdaef7e0699da4de7ca5895b02a170a12d887fd3b17bfdce3481f10bea41f45ba9f709d39ce8325427b57afcfc994cee1b&quot;
</code></pre><p><sup>서명</sup></p></td></tr><tr><td><strong>kaia_connectAndSign</strong>  (<a href="https://eips.ethereum.org/EIPS/eip-191">EIP-191</a>)  지갑 연결<mark style="color:red;"><code>recommended</code></mark><br><a data-footnote-ref href="#user-content-fn-1"><br></a>및 서명을 시작합니다. 사용자에게 지갑<br>제공자를 선택하도록 요청한 후 제공된 메시지에 서명합니다.<br><code>[account, signature]</code> 를 배열로 반환합니다.</td><td>[message: <mark style="color:green;">string</mark>]</td><td><pre class="language-javascript"><code class="lang-javascript">[&quot;account&quot;,&quot;0xa3f20717a250c2b0b729b7e5becbff67fdaef7e0699da4de7ca5895b02a170a12d887fd3b17bfdce3481f10bea41f45ba9f709d39ce8325427b57afcfc994cee1b&quot;]
</code></pre><p><sup>account 및 signature를 Array로 반환</sup></p></td></tr><tr><td><strong>kaia_getBalance</strong> kaia<br><br>잔액을 반환합니다. </td><td><p>[account: <mark style="color:green;">string</mark>, blockNumberOrHash: <mark style="color:green;">string</mark>]<br><br><sup>blockNumberOrHash는 <code>latest</code> 또는 <code>earliest</code>로 설정 가능</sup><br></p><ul><li><sup><code>latest</code>: 가장 최근 블록</sup> </li><li><sup><code>earliest</code>: 제네시스 블록(블록 0)</sup></li></ul></td><td><p><br><br></p><pre class="language-javascript"><code class="lang-javascript">&quot;0x00000000000000000&quot;
</code></pre><p><sup>KAIA 블록체인의 최소 단위인 </sup><a href="https://docs.kaia.io/learn/token-economics/kaia-native-token/#units-of-kaia-"><sup>kei </sup></a><sup>단위의 잔액 값.</sup><br><sup>1 KAIA = 10^18 kei</sup></p></td></tr><tr><td><strong>kaia_sendTransaction</strong> 주어진 매개변수로<br><br>트랜잭션을 생성합니다<br></td><td>[{<br>    from: <mark style="color:green;">string</mark>,<br>    to: <mark style="color:green;">string</mark>,<br>    value: <mark style="color:green;">string</mark>,<br>    gas: <mark style="color:green;">string</mark><br>}]<br><br><sup><code>from</code>필드는 &#x27;kaia_accounts&#x27;<strong>,</strong> &#x27;kaia_requestAccounts&#x27; 또는 &#x27;kaia_connectAndSign&#x27;에서 달성한 계정이어야 합니다.</sup></td><td><p></p><pre class="language-javascript"><code class="lang-javascript">&quot;0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d059210&quot;26d1527331
</code></pre><p><sup>transactionHash</sup></p></td></tr></tbody></table>
#### 오류

```
{code: -32001, message: &#x27;사용자가 취소했습니다&#x27;}
```

<table><thead><tr><th>코드</th><th>설명</th></tr></thead><tbody><tr><td>-32001</td><td><pre class="language-javascript"><code class="lang-javascript">{
  &quot;code&quot;: -32001,
  &quot;message&quot;: &quot;User canceled&quot; 
}
</code></pre><pre class="language-javascript"><code class="lang-javascript">//When the user dismissed the wallet connection popup.
{code: -32001, message: &#x27;User closed popup&#x27;, data: null}
</code></pre><pre class="language-javascript"><code class="lang-javascript">//When the user clicks the dismiss button on the signature popup
{
  &quot;code&quot;: -32001,
  &quot;message&quot;: &quot;User denied message signature&quot;
}
</code></pre><pre class="language-javascript"><code class="lang-javascript">//When the user clicks the dismiss button on the transaction popup
{
  &quot;code&quot;: -32001,
  &quot;message&quot;: &quot;User denied transaction send.&quot;
}
</code></pre></td></tr><tr><td>-32004</td><td>잘못된 발신 주소 (다음 메소드를 실행한 후 다시 시도하십시오 <code>walletProvider.disconnectWallet()</code>)</td></tr><tr><td>-32005</td><td>잘못된 비밀번호 입력으로 인해 사용자가 로그아웃되었습니다 (실행 후 메소드를 다시 시도하십시오) <code>walletProvider.disconnectWallet()</code>)</td></tr><tr><td>-32006</td><td>지갑이 아직 연결되지 않았습니다 (지갑이 연결된 상태에서 오류가 발생한 경우, 실행 후 방법을 다시 시도하십시오 <code>walletProvider.disconnectWallet()</code>. 지갑이 연결되지 않은 상태에서 오류가 발생하면 먼저 지갑을 연결하십시오)</td></tr></tbody></table>
## walletProvider.disconnectWallet()

지갑 연결을 해제합니다.\
이 함수가 호출되면 연결 해제를 확인하는 확인 창이 나타납니다.

```javascript
 const disconnectWallet = async ()=&gt;{
    await walletProvider.disconnectWallet();
    window.location.reload();
}
```

**매개변수**\
\
해당 없음\
\
**반환값**\
\
해당 없음\


<br>
## walletProvider.getErc20TokenBalance()

```javascript
const getErc20TokenBalance = async(contractAddress:string,account:string)=&gt; {
    return await walletProvider.getErc20TokenBalance(contractAddress,account);
}

const USDTContractAddress = &#x27;0xd077a400968890eacc75cdc901f0356c943e4fdb&#x27;;
const account = &#x27;my_account_address&#x27;;
getErc20TokenBalance(USDTContractAddress, account).then(balance =&gt; {
    const formattedUSDTBalance = Number(microUSDTHexToUSDTDecimal(balance as string)).toFixed(2);
    //microUSDTHexToUSDTDecimal은 16진수 문자열을 소수점 문자열로 변환하는 포맷 함수
    //https://github.com/techreadiness/dapp-starter/blob/main/src/utils/format.ts
    console.log(formattedUSDTBalance);
    //0.00
})
```

#### 매개변수

contactAddress <mark style="color:red;">\*필수</mark>
· <mark style="color:green;">문자열</mark>
\
account <mark style="color:red;">\*필수</mark>
· 문자열

#### 응답

64바이트 16진수 문자열.\
반환 값에는 토큰의 `decimals` 사양에 따른 십진수 스케일링이 포함됩니다.

예를 들어, USDT는 10⁶의 십진수 스케일을 사용하는 반면, DELABS는 10¹⁸의 십진수 스케일을 사용합니다.

```
문자열
```

## 호환 라이브러리

* [https://docs.kaia.io/ko/references/sdk/ethers-ext/getting-started/](https://docs.kaia.io/ko/references/sdk/ethers-ext/getting-started/)
* [https://docs.kaia.io/ko/references/sdk/web3js-ext/getting-started/](https://docs.kaia.io/ko/references/sdk/web3js-ext/getting-started/)
* [https://docs.kaia.io/ko/references/sdk/caver-js/](https://docs.kaia.io/ko/references/sdk/caver-js/)

[^1]: <sup>ddd</sup></unknown>
