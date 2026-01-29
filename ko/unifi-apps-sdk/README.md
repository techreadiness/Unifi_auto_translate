---
hidden: true
---

# Unifi Apps SDK

## 1. 시작하기

### 최신 버전

* npm: [https://www.npmjs.com/package/@linenext/dapp-portal-sdk/v/1.5.2](https://www.npmjs.com/package/@linenext/dapp-portal-sdk/v/1.5.2)
* cdn: [https://static.kaiawallet.io/js/dapp-portal-sdk-1.5.2.js](https://static.kaiawallet.io/js/dapp-portal-sdk-1.5.2.js)

### SDK 액세스(clientId 및 clientSecret) 획득 방법

Unifi Apps SDK를 통합하려면 Unifi 팀으로부터 `clientId`와 `clientSecret`을 받아야 합니다.

**단계:**

1.  [SDK 이용 약관 동의서 제출](https://docs.dappportal.io/join-us#mini-dapp-sdk) 시 Unifi Apps 정보를 포함하세요.
2. 제출한 이메일로 `clientId`와 `clientSecret`을 수신하세요.

⚠️ **`clientSecret`을 절대 공개하지 마십시오.** 유출된 경우 기술 지원팀을 통해 재생성을 요청하세요.

### 프로젝트 설정 및 도메인 등록

* `clientId`는 도메인이 등록된 경우에만 활성화됩니다.
  * 테스트 목적으로 `http://localhost:3000`을 사용할 수 있습니다. 
  * 외부 테스트 도메인의 경우 기술 지원팀 또는 이메일을 통해 화이트리스트 등록을 요청하십시오.
* `paymentProvider`를 통한 결제는 유효한 `clientSecret`이 필요합니다.

### SDK 설치

npm, yarn 또는 pnpm을 통해 SDK를 설치하십시오.

```
npm install @linenext/dapp-portal-sdk
# 또는
yarn add @linenext/dapp-portal-sdk
# 또는
pnpm add @linenext/dapp-portal-sdk
```

## 2. SDK 초기화

### SDK 초기화

Unifi Apps가 로드될 때마다 **반드시 SDK를 초기화**해야 합니다.

```javascript
import DappPortalSDK from &#x27;@linenext/dapp-portal-sdk&#x27;

const sdk = await DappPortalSDK.init({
  clientId: &#x27;<client_id>&#x27;,
  chainId: &#x27;1001&#x27;, // 메인넷의 경우 &#x27;8217&#x27;
});
```

**매개변수**

| 이름                                                                       | 설명                                                                                                       |
| -------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
|<p>클라이언트 <mark style="color:$danger;">ID*필수</mark> </p><p>문자열</p>  | SDK 신청 시 제공된 clientId                                                                   |
|                                                <p>체인 ID </p><p>문자열</p>| 기본값은 **1001**(테스트넷)입니다. 개발 후 메인넷을 사용하려면 값을 **8217**(메인넷)으로 설정하세요. |

**응답**

다음 메서드를 호출할 수 있는 `DappPortalSDK` 객체를 반환합니다.

```
DappPortalSDK
```

### **⚠️ LINE MINI 앱 및 LINE 로그인 LIFF 버전 참고사항**

* `DappPortalSDK.init()` 호출 **전**에 `liff.init()`를 호출하세요.
* LINE MINI 앱 또는 LINE 로그인 LIFF 진입 시 지갑 연결(`connectWallet`)을 **트리거하지 마세요**. 필요한 경우에만 연결하세요(예: 아이템 구매, 온체인 보상).
* 이는 LINE을 통한 활성 사용자 추적 및 어트리뷰션의 정확성을 보장합니다.

### 💡 **권장 사항**

* **SDK는 단 한 번만 초기화**하고 `DappPortalSDK` 인스턴스를 **싱글톤**으로 관리하십시오.
* `DappPortalSDK.init()`을 여러 번 호출하지 마십시오—**예상치 못한 동작이나 오작동**을 유발할 수 있습니다.

기본적으로 싱글톤 사용을 **강제하지 않음**. 이는 **다중 구성 설정**(예: 단일 앱에서 **테스트넷**과 **메인넷** 동시 사용)을 허용하기 위함입니다.
이러한 경우 **구성당 하나의 싱글톤 인스턴스**를 관리하십시오(예: 테스트넷용 하나, 메인넷용 하나).

## 3. SDK API 참조

### **DappPortalSDK 클래스**

#### **생성자**

`DappPortalSDK(config: DappPortalSDKClientConfig)`

인증 정보를 사용하여 SDK를 초기화합니다.

* `clientId: string` (Unifi 팀에서 제공)
* `chainId: string` (테스트넷: &quot;1001&quot;, 메인넷: &quot;8217&quot;)

#### **인스턴스 메서드**

**`getWalletProvider(): WalletProvider`**

EIP-1193 호환 지갑 제공자 인스턴스를 반환합니다.

* 이를 통해 트랜잭션 전송, 메시지 서명, 지갑 상호작용이 가능합니다.

**`getPaymentProvider(): PaymentProvider`**

결제 및 트랜잭션 내역 관리를 위한 객체를 반환합니다.

**`isSupportedBrowser(): boolean`**

현재 브라우저의 호환성을 확인합니다.

**`showUnsupportedBrowserGuide(): Promise<void>`**

지원되는 브라우저에서 열도록 사용자에게 안내하는 가이드를 표시합니다.

## 4. 보안 지침

* `clientSecret`을 기밀로 유지하십시오.
* 소스 제어에 절대 커밋하지 마십시오.
* 노출된 경우 즉시 기술 지원팀을 통해 교체하십시오.</void></client_id>
