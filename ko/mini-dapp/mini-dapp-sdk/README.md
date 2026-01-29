# 미니 앱 SDK

## 인증

미니 앱 SDK를 통합하려면 미니 앱이 `clientId`와 `clientSecret`을 반드시 획득해야 합니다. 이 자격 증명은 서비스 도메인이 `clientId`에 등록된 후 활성화될 수 있습니다.

## 프로젝트 생성

미니 앱을 공식적으로 오픈하려면 서비스 도메인 등록이 필수입니다. 서비스 도메인을 획득한 후 등록을 요청하십시오.

애플리케이션용 서비스 도메인이 구축되지 않은 경우, 테스트를 위해 로컬 환경 경로를 사용할 수 있습니다. `http://localhost:3000`를 사용하십시오.

페이먼트 프로바이더를 사용하려면 `clientSecret`이 필요합니다. **`clientSecret`을 공개적으로 공유하지 마십시오.** 노출된 경우, 새 `clientSecret` 발급을 요청하십시오.

## SDK 설치

npm 또는 yarn을 통해 프로젝트에 Mini Dapp SDK를 추가하세요.

```
npm install @linenext/dapp-portal-sdk
```

또는

```
yarn add @linenext/dapp-portal-sdk
```

## SDK 초기화

<mark style="color:red;">**미니 앱 실행 시 반드시 DappPortalSDK.Init()를 호출해야 합니다. LIFF 버전의 경우 liff.init() 완료 후 수행해야 합니다.**</mark> 

이 단계에서는 `DappPortalSDK.Init()`까지만 구현하면 되며, 미니 앱 연결 완료는 **필수**가 아닙니다.  \
LIFF 환경 내 미니 앱 연결(지갑 연동)은 **필요한 경우에만**(예: 온체인 보상 수령, 아이템 구매 시) 실행해야 하며, LIFF 초기 진입 시에는 실행하지 않습니다.

* 배경 : 이 접근 방식은 미니 앱 내 활성 사용자 검증 데이터를 처리하기 위해 필요합니다. 이 데이터는 성과 측정 및 사용자 확보 전략 수립에 중요합니다.
* 주의사항 : 본 가이드를 따르면 미니 앱에 연결된 LINE 사용자의 암호화된 정보가 LINE NEXT에 제공됩니다.

## class DappPortalSDK

#### 1. DappPortalSDK(config: DappPortalSDKClientConfig)

* clientId를 사용하여 SDK 초기화.
* 사전에 제공된 clientId를 사용합니다. SDK는 사전 협의된 호스트 주소에서만 실행됩니다.

#### DappPortalSDKClientConfig

* clientId: string
* chainId: string
* SDK는 기본적으로 프로덕션 환경에서 실행됩니다. 테스트넷 연결을 원할 경우 _‘1001’_을 사용하십시오.

#### 2. getWalletProvider(): WalletProvider

* EIP-1193 인터페이스와 호환되는 WalletProvider를 얻을 수 있습니다.

#### 3. getPaymentProvider() : PaymentProvider

* 결제 처리 및 내역을 지원하는 PaymentProvider를 얻을 수 있습니다.

#### 4. isSupportedBrowser(): boolean

* SDK와 브라우저 간 호환성을 검증하는 함수입니다.

#### 5. showUnsupportedBrowserGuide(): Promise

* 현재 브라우저가 지원되지 않을 경우 외부 브라우저 사용 방법을 안내하는 화면을 표시합니다.
