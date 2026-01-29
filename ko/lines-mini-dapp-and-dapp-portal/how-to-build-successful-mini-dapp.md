# 성공적인 미니 앱 구축 방법

## Dapp 포털에 노출되기 위한 조건

미니 앱이 온보딩 과정에서 아래 요구사항을 충족할수록 Dapp 포털에 노출될 가능성이 높아지고 더 많은 사용자를 유치할 수 있습니다. 미니 앱 개발 시 반드시 요구사항을 준수해 주시기 바랍니다.

## 필수 요건

### Mini Dapp Connect를 통한 다양한 환경에서의 서비스 제공

클라이언트는 LINE 버전과 웹 버전, 두 가지 유형의 Mini Dapp을 구축해야 합니다. 

<figure><img src="../.gitbook/assets/스크린샷 2025-02-06 오전 9.50.03.png" alt=""><figcaption><p>Web3.0 PvsZ | 미니 앱</p></figcaption></figure>#### LINE 버전

LINE 버전은 LIFF SDK를 통해 구축 가능합니다. 사용자는 앱 설치나 다운로드 없이 LINE 메신저를 통해 미니 앱에 쉽게 접근할 수 있습니다. 또한 LINE 계정으로 로그인하여 친구 초대 및 지갑 생성이 가능합니다.

LINE 버전 접근 시 사용자 이탈률을 낮추기 위해, 초기 화면보다는 필요 시에만 Wallet Connect를 제공하는 것을 강력히 권장합니다. 다만 보상 제공 시 지갑 연동이 필수적일 수 있으므로, 지갑 연동 버튼은 쉽게 찾을 수 있는 위치에 배치하는 것이 좋습니다.

사용자 흐름 : \
미니 앱(LIFF) 접속 -&gt; 채널 동의 -&gt; OA 추가 -&gt; 미니 앱 플레이 -&gt; 지갑 연결 (결제, 보상 등 필요한 단계에서)

<figure><img src="../.gitbook/assets/스크린샷 2025-02-11 오후 2.56.51.png" alt=""><figcaption><p>Web3.0 PvsZ | 미니 앱</p></figcaption></figure>#### 웹 버전

LINE 메신저에 익숙하지 않은 사용자를 위해 미니 앱은 웹 버전으로도 구축되어야 합니다. 미니 앱 SDK는 다양한 소셜 계정, Kaia Wallet(모바일 앱/확장 프로그램), OKX Wallet을 통한 지갑 연결을 포함한 웹 환경 통합을 제공합니다.

웹 버전의 경우, 계정 생성 초기 화면에 Wallet Connect를 제공해야 합니다. Wallet Connect는 LINE 로그인을 의미하지 않으며, 미니 앱 SDK를 통해 제공되는 지갑 연동을 의미합니다.

사용자 흐름 : \
미니 앱(웹) 접속 -&gt; Wallet Connect -&gt; 미니 앱 실행

<figure><img src="../.gitbook/assets/스크린샷 2025-02-11 오후 3.09.14.png" alt=""><figcaption><p>Web3.0 PvsZ | 미니 앱</p></figcaption></figure>#### LINE과 웹 버전 간 호환성

미니 앱 두 버전의 계정 시스템은 버전 간 계정 호환성을 보장하기 위해 지갑 주소를 기반으로 운영되어야 합니다.

LIFF 및 웹 버전에서 지갑 연결 시, 미니앱 지갑(LINE) 또는 OKX 지갑으로 연결이 진행되면 지갑 주소가 양 버전에서 동일하게 유지되어 계정 정보 호환성이 보장됩니다.\
단, 웹 버전의 미니앱 지갑(Kaia Wallet 앱/확장 프로그램 및 LINE 제외 소셜 로그인)은 LIFF 버전과 호환되지 않습니다.

<figure><img src="../.gitbook/assets/Wallet_Compatibility.png" alt=""><figcaption></figcaption></figure>_예를 들어, 사용자 A가 웹 버전에서 LINE 계정 &#x27;a&#x27;로 미니 앱 지갑을 생성한 경우, LINE 메신저에 LINE 계정 &#x27;a&#x27;로 로그인한 경우 LIFF와 동일합니다._

### 인앱 아이템 스토어 제공

미니 앱 SDK는 암호화폐($KAIA)와 Fait(STRIPE) 결제 솔루션을 모두 제공합니다. 수익 모델을 구축하려면 인앱 아이템 스토어를 설정해야 합니다.

<figure><img src="../.gitbook/assets/스크린샷 2025-02-06 오전 10.23.29.png" alt=""><figcaption><p>위즈우즈 | 미니 앱, 미드나이트 서바이버스 | 미니 앱</p></figcaption></figure>### 다국어 지원

미니 앱은 기본적으로 영어와 일본어를 제공해야 합니다. 타겟 국가에 따라 다른 언어를 선택적으로 제공할 수 있습니다. 사용자 국가 분류는 여러 방법으로 가능합니다. 사용자가 설정한 브라우저 또는 시스템 언어 설정을 따르거나 접속 IP 주소를 기반으로 국가를 판단할 수 있으며, 이에 따라 적절한 언어를 제공해야 합니다.

<figure><img src="../.gitbook/assets/MiniDapp_Multi.png" alt=""><figcaption><p>Dapp 포털</p></figcaption></figure>### 포인트 보상 제공

포인트 보상은 사용자 충성도를 높일 수 있습니다. 이러한 포인트는 미니 앱 내에서 화폐로 사용될 수 있으며, 궁극적으로 미니 앱에서 발행한 토큰과의 교환을 지원하여 경제적 이익감을 제공합니다. 이는 미니 앱의 폭발적인 성장으로 이어질 수 있습니다.

<figure><img src="../.gitbook/assets/스크린샷 2025-02-06 오전 10.43.32.png" alt=""><figcaption><p>Bombie | 미니 앱, Heroicarena | 미니 앱, SuperZ | 미니 앱</p></figcaption></figure>### 연결된 지갑 정보 제공

미니 앱의 모든 화면에서 연결된 지갑 정보를 사용자에게 명확히 알리는 것이 매우 중요합니다. 사용자는 여러 미니 앱을 즐기며 각 앱마다 다른 지갑을 연결할 수 있습니다. 어떤 지갑이 연결되었는지, 잔액이 얼마인지 직관적으로 제공함으로써 결제까지 이어지는 편의성을 높일 수 있습니다.

<figure><img src="../.gitbook/assets/Connected_Wallet.png" alt=""><figcaption><p>Elderglade | 미니 앱</p></figcaption></figure>* 지갑 유형 : [getWalletType()](https://docs.dappportal.io/mini-dapp/mini-dapp-sdk/wallet-provider#a.-getwallettype-wallettype-or-null)
* 지갑 주소 : [kaia\_accounts()](https://docs.dappportal.io/mini-dapp/mini-dapp-sdk/wallet-provider#b.-async-request-requestargs-requestarguments-promise)
  * 연결된 지갑이 없는 경우 kaia\_requestAccounts() 사용
* 지갑 잔액 : [kaia\_getBalance()](https://docs.kaia.io/ko/references/json-rpc/kaia/get-balance/)

### 결제 상태 제공

사용자에게 결제 진행 상태를 알리는 것은 매우 중요합니다. 결제 생성 API를 사용하여 결제를 시작한 후, 결제 게이트웨이(PG)와의 통신을 통해 결제가 처리되고 완료됩니다. 사용자 화면에 결제 완료 및 아이템 배포 알림이 적절히 제공되지 않으면 결제가 완료되었는지 확인할 수 없습니다. 결제 시작 시 결제 진행 중 상태를 보여주는 UI를 제공해야 하며, 결제 완료 웹훅 수신 시 결제 화면에 아이템 배포 과정을 표시해야 합니다.

<figure><img src="../.gitbook/assets/PaymentProcess.png" alt=""><figcaption><p>Elderglade | 미니 Dapp</p></figcaption></figure>* [결제 생성 API &gt;](https://docs.dappportal.io/mini-dapp/mini-dapp-sdk/payment-provider#id-01.-payment)
* [결제 상태 &gt;](https://docs.dappportal.io/mini-dapp/mini-dapp-sdk/payment-provider#id-05.-payment-status) 

### 가로 모드 기반 미니 앱 가이드

<figure><img src="../.gitbook/assets/MiniDapp_Portrait.png" alt=""><figcaption><p>Snake Online | 미니 앱</p></figcaption></figure>미니 앱이 가로 모드에 최적화된 경우, 사용자의 기기가 세로 모드로 설정되어 있을 때에도 가로 모드로 작동하도록 하십시오. 자동 회전 기능이 사용될 때에도 가로 모드에서 정상 작동해야 합니다.

### 홈 화면에 추가

<figure><img src="../.gitbook/assets/AddToHome.png" alt=""><figcaption><p>홈 화면에 추가 | Dapp 포털</p></figcaption></figure>Dapp 포털은 사용자가 모바일 홈 화면에서 미니 Dapp에 쉽게 접근할 수 있는 바로가기를 제공합니다.

&quot;홈 화면에 추가&quot; 기능은 두 가지 방식으로 제공됩니다:

1. Dapp 포털 내 미니 Dapp 상세 화면에서 이용 가능.
2. **미니 Dapp에서 제공 (바로 가기 URL은 Dapp 포털에서 제공되며, 미니 Dapp은 이 URL을 통합할 UI를 개발합니다).**
   1. 바로 가기 URL : https://www.dappportal.io/shortcut.html?dappId=`dappId`\®ister;=1&amp;\&amp;openExternalBrowser;=1\
      \*`dappId`: 브릿지 페이지 URL에서 확인하거나, 없는 경우 지원 채널에 문의하십시오.\
      \*register=1: 필수.\
      \*openExternalBrowser=1: LIFF에서 URL을 열 경우 외부 브라우저에서 열 수 있도록 허용합니다.

<figure><img src="../.gitbook/assets/MiniDapp_ATH.png" alt=""><figcaption><p>Mini Dapp에서 제공하는 홈 화면에 추가</p></figcaption></figure>### 유지보수 모드 제공

<figure><img src="../.gitbook/assets/스크린샷 2025-05-20 오후 12.59.40.png" alt="" width="224"><figcaption><p>유지보수 모드 | 예시</p></figcaption></figure>미니 앱의 정기 또는 긴급 유지보수 시 사용자 경험을 향상시키기 위해 유지보수 화면을 제공해 주십시오. 유지보수 중이나 접근 불가 시 어떠한 알림도 없을 경우 사용자에게 혼란을 초래할 수 있습니다.\
유지보수 화면에 **예상 종료 시간과 상세 업데이트를 위한 연락처 정보**를 포함하는 것이 도움이 될 것입니다.<br>

### 닫기 확인 대화상자 제공

미니 앱 실행 중 사용자가 실수로 뒤로 가기 버튼을 누르면 현재 진행 상황이 저장되지 않고 미니 앱이 예기치 않게 종료될 수 있습니다. 페이지가 닫히기 직전에 확인 팝업을 표시하는 것이 권장됩니다.

<p align="center"><img src="../.gitbook/assets/66 (4).jpg" alt=""><br></p>다음 코드를 사용하여 확인 팝업을 표시할 수 있습니다:

#### 예시 (React)

랜딩 페이지 또는 레이아웃 컴포넌트에 다음 코드를 삽입하세요:

```javascript

useEffect(() =&gt; {
    const preventGoBack = () =&gt; {
        if(window.location.pathname === &#x27;/&#x27;) {
            const isConfirmed = confirm(&#x27;정말 뒤로 가시겠습니까?&#x27;);
            if (!isConfirmed) {
                history.pushState(null, &#x27;&#x27;, window.location.pathname)
            }
        }
    };

    window.addEventListener(&#x27;popstate&#x27;, preventGoBack);

    // 언마운트 시 리스너 제거
    return () =&gt; {
        window.removeEventListener(&#x27;popstate&#x27;, preventGoBack);
    };
}, []);

```

#### 예시 (순수 자바스크립트 - `index.html`)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>뒤로 가기 버튼 차단기</title>
</head>
<body>
  <h1>홈</h1>

  <script>
    if (window.location.pathname === &#x27;/&#x27;) {
      history.pushState(null, &#x27;&#x27;, window.location.pathname);
    }

    function preventGoBack(event) {
      if (window.location.pathname === &#x27;/&#x27;) {
        const isConfirmed = confirm(&#x27;Are you sure you want to go back?&#x27;);
        if (!isConfirmed) {
          history.pushState(null, &#x27;&#x27;, window.location.pathname);
        }
      }
    }

    window.addEventListener(&#x27;popstate&#x27;, preventGoBack);

    window.addEventListener(&#x27;beforeunload&#x27;, () =&gt; {
      window.removeEventListener(&#x27;popstate&#x27;, preventGoBack);
    });
  </script>
</body>
</html>
```
