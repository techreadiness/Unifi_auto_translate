---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/unifi-apps-demo/unifi-apps-starter
---

# Unifi Apps Starter

미니 앱 개발이 처음이라면 어디서부터 시작해야 할지 막막할 수 있습니다. Unifi Apps Starter는 이러한 개발자들을 위한 훌륭한 출발점입니다.

Unifi Apps Starter는 미니 앱 구축에 필요한 필수 기능을 모두 포함한 템플릿입니다. 이 템플릿을 기반으로 자유롭게 커스터마이징하여 귀사만의 미니 앱을 효율적으로 개발할 수 있습니다.

본 가이드는 Unifi Apps Starter의 활용 방법을 다음 순서대로 안내합니다.



1. [Unifi Apps Starter란?](unifi-apps-starter.md#what-is-the-unifi-apps-starter)
2. [시작하기](unifi-apps-starter.md#how-to-get-started-with-the-unifi-apps-starter)

* 개발 환경 설정 (Environment setup)
* 소스 코드 다운로드 및 실행 (Downloading and running the source code)
* 서버 배포 (Deploying to a server)

3. [주요 기능](unifi-apps-starter.md#key-features-of-the-unifi-apps-starter)

* 지갑 연결 및 해제 (Connect/disconnect wallet)
* 암호화폐 및 법정화폐(Fiat) 결제 (Crypto/fiat payment)
* KAIA/STRIPE 교환 비율(Conversion Ratio) 확인
* LIFF 연동 (LIFF integration)

## Unifi Apps Starter란?

Unifi Apps Starter는 개발자가 `dapp-portal-sdk`를 쉽고 빠르게 통합할 수 있도록 설계된 템플릿 프로젝트입니다. 프로젝트를 처음부터(Scratch) 직접 구축할 수도 있지만, 이 스타터를 활용하면 훨씬 효율적이고 원활한 개발 경험을 얻을 수 있습니다.

또한 미리 정의된 디자인 가이드를 따르고 있어, UI/UX의 일관성을 유지하는 데 도움이 됩니다.

이 프로젝트는 Next.js 기반으로 구축되었습니다. 만약 다른 프레임워크를 사용할 계획이더라도, 이 리포지토리는 `dapp-portal-sdk` 연동 방식을 이해하는 데 유용한 참조 자료(Reference)가 될 것입니다.<br>

## 시작하기

1. **환경 설정 (Environment setup)**

Unifi Apps Starter를 실행하려면 Node.js가 필요합니다. 패키지 매니저는 pnpm을 사용합니다 (npm과 호환 가능).

* 권장 Node.js 버전: 20.0.0 이상
* &#x20;`.nvmrc` 에 명시된 버전: v20.18.0

⚠️ 주의: 이전 버전에서도 일부 기능이 작동할 수 있으나, Netlify 배포 도구와의 호환성을 보장하기 위해 Node.js 20.0.0 이상 사용을 필수로 권장합니다.

\*_Tip_: [`nvm`](https://github.com/nvm-sh/nvm) 을 사용하면 Node 버전을 손쉽게 관리할 수 있습니다.



2. **소스 코드 다운로드 및 실행 (Downloading and running the source code)**

GitHub에서 리포지토리를 Clone하거나 Fork할 수 있습니다.\
[ https://github.com/techreadiness/unifi-apps-starter](https://github.com/techreadiness/unifi-apps-starter)

로컬 환경에서 프로젝트를 실행하려면, 리포지토리 내의 `README.md` 파일에 기재된 지침을 따라주세요.

### 서버 배포 (Deploying to a server)

로컬 환경에서 Unifi Apps Starter를 실행하고 정상 작동을 확인했다면, **Netlify**를 사용하여 라이브 서버에 배포할 수 있습니다.

<details>

<summary>배포를 진행하려면 Netlify 계정이 필요합니다.</summary>

[Netlify (opens new window)](https://www.netlify.com/)는 정적 사이트(Static Site)를 위한 호스팅 서비스입니다. 배포를 시작하기 전에 미리 계정을 생성해 주세요.

> 📌 참고: 이 프로젝트는 Netlify의 무료 플랜(Free plan)에서도 문제없이 실행할 수 있습니다.

</details>

```bash
# 루트 디렉토리로 이동
cd ./
# 프로젝트 빌드
pnpm build
# 초안(Draft/Preview) 환경에 배포
netlify deploy
# 검증 완료 후, 프로덕션(Production) 환경에 배포
netlify deploy --prod
```

## Unifi Apps Starter의 주요 기능 (Key features)

Unifi Apps Starter에는 몇 가지 기본 기능이 사전에 구현(Out of the box)되어 있습니다. 이는 `dapp-portal-sdk`의 핵심 기능을 사용하는 방법을 보여주는 예시이며, 최종 솔루션이 아닌 "참조 코드(Reference Code)"로 활용하시기 바랍니다.

### **1. 지갑 연결/해제 (Connect/Disconnect wallet)**

지갑을 연결하고 해제하는 것은 SDK 사용의 가장 기초적인 기능입니다. 코드 내에서 `walletProvider`와 관련 메서드들을 어떻게 사용하는지 확인할 수 있습니다.

### **2. 암호화폐/법정화폐 결제 (Crypto/Fiat payment)**

이 템플릿은 `paymentProvider`를 사용하여 암호화폐(Crypto)와 법정화폐(Fiat) 결제를 모두 처리하는 방법을 보여줍니다. 다음과 같은 예시가 포함되어 있습니다.

* `paymentId` 생성 (Creating paymentId)
* 결제 상태 확인 (Checking the payment status)
* 결제 완료 처리 (Finalizing the payment)

### **3. KAIA/STRIPE 환율 변환 (KAIA/STRIPE ratio)**

결제를 지원하기 위해서는 암호화폐(KAIA)와 법정화폐(STRIPE) 간의 적절한 가격 변환 로직을 적용해야 합니다. 스타터에는 참조용으로 `usd-to-kaia` 함수가 포함되어 있습니다.

### **4. LIFF 통합 (LIFF integration)**

LINE Front-end Framework (LIFF) 연동을 계획 중이라면, 이 프로젝트에서 유용한 예시를 찾을 수 있습니다.

* LIFF 초기화 시점 (When to initialize LIFF)
* `shareTargetPicker`와 같은 메서드 사용 방법
