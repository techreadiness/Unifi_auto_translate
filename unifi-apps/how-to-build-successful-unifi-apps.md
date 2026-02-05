---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/unifi-apps-review-guidelines/how-to-build-successful-unifi-apps
---

# 성공적인 유니파이 앱 구축 방법

## 유니파이 추천 앱 선정 기준

앱 등록 시 아래 요구사항을 충족할수록 유니파이 추천 앱으로 선정되어 더 많은 사용자를 유치할 가능성이 높아집니다. 유니파이 앱 개발 시 반드시 해당 요구사항을 준수해 주시기 바랍니다.

## 필수 요건

### Unifi Apps Connect를 통한 다양한 환경에서의 서비스 제공

**지원 가능한 버전 조합**

* LINE MINI 앱 &amp; LINE 로그인 LIFF &amp; 웹
* LINE MINI 앱 &amp; 웹
* LINE 로그인 LIFF &amp; 웹
* LINE MINI 앱 또는 웹 (단일 유형)

<figure><img src="../.gitbook/assets/스크린샷 2025-02-06 오전 9.50.03.png" alt=""><figcaption><p>Web3.0 PvsZ | 유니피 앱</p></figcaption></figure>#### LINE 버전 (LINE MINI 앱 또는 LINE 로그인 LIFF)

LINE 버전은 **LIFF SDK**를 활용하여 구축할 수 있으며, 사용자는 **별도의 애플리케이션 설치나 다운로드 없이 LINE 메신저를 통해 직접 Unifi Apps에 접근**할 수 있습니다.
사용자는 **로그인한 LINE 계정으로 친구 초대 및 지갑 생성**이 가능하여 원활한 온보딩 경험을 제공합니다.

LINE 버전 접근 시 사용자 이탈을 줄이기 위해, **초기 화면에서 Wallet Connect를 피할 것을 강력히 권장**하며, **필요한 경우에만 활성화**하시기 바랍니다.
다만 **결제나 보상**과 같은 기능에는 지갑 연동이 필요할 수 있으므로, 지갑 연결 진입점은 필요 시 **명확히 표시되고 쉽게 접근 가능**해야 합니다.

**사용자 흐름 :** 

* LINE MINI 앱
  * `유니파이 앱 접근(LINE MINI 앱) → 유니파이 앱 실행 → 지갑 연결(예: 결제 또는 보상 단계에서)`
* LINE 로그인 LIFF
  * `유니파이 앱 접근(LINE 로그인 LIFF) → 채널 동의 → 공식 계정 추가 → 유니파이 앱 실행 → 지갑 연결(예: 결제 또는 보상 단계에서)`

<figure><img src="../.gitbook/assets/스크린샷 2025-02-11 오후 2.56.51.png" alt=""><figcaption><p>Web3.0 PvsZ | 유니파이 앱</p></figcaption></figure>#### 웹 버전

**LINE 메신저에 익숙하지 않은** 사용자 지원을 위해 유니피 앱은 **웹 버전**으로도 제공되어야 합니다.\
유니피 앱 SDK는 **다양한 소셜 계정을 통한 지갑 연결**, **카이아 월렛(모바일 앱 및 브라우저 확장 프로그램)**, **OKX 월렛**, **비트겟 월렛**을 포함한 웹 기반 연동을 지원합니다.

웹 버전의 경우, 계정 생성을 가능하게 하기 위해 **초기 화면에서 Wallet Connect가 반드시 제공되어야 합니다**.
**Wallet Connect는 LINE 로그인을 의미하지 않으며**, **Unifi Apps SDK가 제공하는 지갑 통합 기능**을 가리킵니다.

**사용자 흐름 :** \
`Unifi Apps(웹) 접속 → Wallet Connect → Unifi Apps 실행`

<figure><img src="../.gitbook/assets/스크린샷 2025-02-11 오후 3.09.14.png" alt=""><figcaption><p>Web3.0 PvsZ | Unifi Apps</p></figcaption></figure>### 인앱 아이템 스토어 제공

**Unifi Apps SDK**는 **인앱 구매(IAP)**, **암호화폐**, **법정화폐** 결제를 포함한 다양한 결제 솔루션을 제공합니다.\
지속 가능한 수익 모델 구축을 위해 서비스는 지원되는 플랫폼 버전에 따라 적절한 결제 방식을 활용한 **인앱 아이템 스토어**를 제공해야 합니다.

#### 플랫폼별 결제 방식

지원되는 결제 방식은 온보딩 버전에 따라 다릅니다:

* **LINE MINI 앱**
  * **인앱 구매(IAP)**를 주요 결제 방식으로 반드시 제공해야 합니다.
  * LINE MINI 앱 버전에서는 암호화폐 및 법정화폐 결제가 **지원되지 않습니다**.
* **LINE 로그인 LIFF &amp; 웹**
  * **암호화폐 및 법정화폐 결제 방식**을 반드시 제공해야 합니다.
  * 지원되는 결제 옵션은 Unifi Apps SDK를 통해 제공되는 암호화폐 결제($KAIA, USDT) 및 STRIPE를 통한 법정화폐 결제를 포함합니다.

<figure><img src="../.gitbook/assets/스크린샷 2025-02-06 오전 10.23.29.png" alt=""><figcaption><p>Wizzwoods | Unifi Apps, Midnight Survivors | Unifi Apps</p></figcaption></figure>### 다국어 지원

Unifi Apps는 기본적으로 영어와 일본어를 제공해야 합니다. 타겟 국가에 따라 다른 언어는 선택적으로 제공 가능합니다. 사용자 국가 분류는 여러 방법으로 수행할 수 있습니다. 사용자가 설정한 브라우저 또는 시스템 언어 설정을 따르거나 접속 IP 주소를 기반으로 국가를 판단할 수 있으며, 이에 따라 적절한 언어를 제공해야 합니다.

<figure><img src="../.gitbook/assets/MiniDapp_Multi.png" alt=""><figcaption><p>Unifi</p></figcaption></figure>### 포인트 보상 제공

포인트 보상은 사용자 충성도를 높일 수 있습니다. 이 포인트는 유니피 앱 내에서 화폐로 사용될 수 있으며, 궁극적으로 유니피 앱에서 발행한 토큰과의 교환을 지원하여 경제적 이익을 제공합니다. 이는 유니피 앱의 폭발적인 성장을 이끌 수 있습니다.

<figure><img src="../.gitbook/assets/스크린샷 2025-02-06 오전 10.43.32.png" alt=""><figcaption><p>Bombie | Unifi Apps, Heroicarena | Unifi Apps, SuperZ | Unifi Apps</p></figcaption></figure>### 연결된 지갑 정보 제공

Unifi 앱의 모든 화면에서 사용자에게 연결된 지갑 정보를 인지시키는 것이 매우 중요합니다. 사용자는 여러 Unifi 앱을 이용하며 각 앱마다 다른 지갑을 연결할 수 있습니다. 어떤 지갑이 연결되어 있고 잔액이 얼마인지 직관적인 정보를 제공함으로써 결제까지 이어지는 편의성을 높일 수 있습니다.

<figure><img src="../.gitbook/assets/Connected_Wallet.png" alt=""><figcaption><p>Elderglade | Unifi Apps</p></figcaption></figure>* 지갑 유형 : [getWalletType()](https://docs.dappportal.io/unifi-apps-sdk/wallet-provider#walletprovider.getwallettype)
* 지갑 주소 : [kaia\_accounts()](https://docs.dappportal.io/unifi-apps-sdk/wallet-provider#walletprovider.request)
  * 연결된 지갑이 없는 경우 kaia\_requestAccounts() 사용
* 지갑 잔액 : [getErc20TokenBalanceWithDepositedBalance()](https://docs.dappportal.io/unifi-apps-sdk/wallet-provider#walletprovider.geterc20tokenbalancewithdepositedbalance)

### 결제 상태 제공

사용자가 **현재 결제가 어떤 단계에 있는지** 명확히 이해하는 것이 중요합니다.

결제 생성 API를 통해 결제가 시작되면, 결제 게이트웨이(PG)와의 통신을 통해 처리 및 완료됩니다.
결제 결과나 아이템 배포 상태가 화면에 명확히 표시되지 않으면, 사용자는 결제가 성공적으로 완료되었는지 확신하지 못할 수 있습니다.

혼란을 방지하기 위해 다음과 같은 UI 흐름을 제공해야 합니다:

* **결제 처리 중**에는 결제가 진행 중임을 명확히 표시하는 UI를 표시합니다(예: &quot;결제 진행 중&quot;).
* **결제 완료 웹훅 수신 후**, 화면에 아이템 배포 과정을 표시합니다.
* 아이템 배포가 완료되면 사용자에게 프로세스가 끝났음을 명확히 알립니다.

사용자는 화면에서 전체 흐름을 쉽게 따라갈 수 있어야 합니다:\
**결제 진행 중 → 결제 완료 → 아이템 배송 완료**

<figure><img src="../.gitbook/assets/PaymentProcess.png" alt=""><figcaption><p>Elderglade | Unifi Apps</p></figcaption></figure>* [결제 생성 API &gt;](https://docs.dappportal.io/unifi-apps-sdk/payment-provider#id-1.-triggering-createpayment-api-from-mini-dapp)
* [결제 상태 조회 &gt;](https://docs.dappportal.io/unifi-apps-sdk/payment-provider#id-3.-payment-status-change-event) 

### 가로 모드 기반 유니피 앱 가이드

유니피 앱이 가로 모드에 최적화된 경우, 사용자의 기기가 세로 모드로 설정되어 있을 때에도 가로 모드로 작동하도록 하십시오. 자동 회전 기능이 사용될 때에도 가로 모드에서 정상 작동해야 합니다.

<figure><img src="../.gitbook/assets/MiniDapp_Portrait.png" alt=""><figcaption><p>Snake Online | Unifi Apps</p></figcaption></figure>### 홈 화면에 추가

<figure><img src="../.gitbook/assets/AddToHome.png" alt=""><figcaption><p>홈 화면에 추가 | Unifi</p></figcaption></figure>유니피는 사용자가 모바일 홈 화면에서 유니피 앱에 쉽게 접근할 수 있는 바로가기를 제공합니다.

&quot;홈 화면에 추가&quot; 기능은 두 가지 방식으로 제공됩니다:

1. 유니피 내 유니피 앱 상세 화면에서 이용 가능.
2. **Unifi 앱에서 제공 (바로 가기 URL은 Unifi에서 제공하며, Unifi 앱은 이 URL을 통합할 UI를 개발합니다).**
   1. 바로 가기 URL : https://www.dappportal.io/shortcut.html?dappId=`dappId`\®ister;=1&amp;\&amp;openExternalBrowser;=1\
      \*`dappId`: 브릿지 페이지 URL에서 확인하거나, 없는 경우 지원 채널에 문의하십시오.\
      \*register=1: 필수.\
      \*openExternalBrowser=1: LINE 로그인 LIFF에서 URL을 열 경우 외부 브라우저에서 열 수 있도록 허용합니다.

<figure><img src="../.gitbook/assets/MiniDapp_ATH.png" alt=""><figcaption><p>Unifi Apps에서 제공하는 홈 화면에 추가</p></figcaption></figure>### 유지보수 모드 제공

<figure><img src="../.gitbook/assets/스크린샷 2025-05-20 오후 12.59.40.png" alt="" width="224"><figcaption><p>유지보수 모드 | 예시</p></figcaption></figure>Unifi Apps의 정기 또는 긴급 유지보수 시 사용자 경험을 향상시키기 위해 유지보수 화면을 제공해 주십시오. 유지보수 중이나 접근 불가 시 어떠한 알림도 없을 경우 사용자에게 혼란을 초래할 수 있습니다.\
유지보수 화면에 **예상 종료 시간과 상세 업데이트를 위한 연락처 정보**를 포함하는 것이 도움이 될 것입니다.<br>

### 닫기 확인 대화상자 제공

사용자가 Unifi Apps 실행 중 실수로 뒤로 가기 버튼을 누르면 현재 진행 상황이 저장되지 않고 Unifi Apps가 예기치 않게 종료될 수 있습니다. 페이지가 닫히기 직전에 확인 팝업을 표시하는 것이 권장됩니다.

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
