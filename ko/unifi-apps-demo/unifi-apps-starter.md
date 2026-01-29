# 유니파이 앱 스타터

미니 앱 개발을 시작하는 것은 어려울 수 있습니다. 유니파이 앱 스타터는 프로젝트를 빠르게 시작할 수 있는 견고한 기반을 제공합니다.

이 템플릿에는 미니 앱 구축에 필요한 핵심 기능이 포함되어 있어 효율적으로 사용자 정의하고 자체 애플리케이션을 구축할 수 있습니다. 이 가이드에서는 다음을 다룹니다:

* [유니파이 앱 스타터란?](unifi-apps-starter.md#what-is-the-unifi-apps-starter)
* [시작하기](unifi-apps-starter.md#how-to-get-started-with-the-unifi-apps-starter) (환경 설정, 소스 코드, 배포)
* [주요 기능](unifi-apps-starter.md#key-features-of-the-unifi-apps-starter) (지갑 연결, 결제, LIFF 통합)

## 유니피 앱 스타터란 무엇인가요?

**유니피 앱 스타터**는 `dapp-portal-sdk`를 쉽게 통합할 수 있도록 설계된 템플릿 프로젝트입니다. 미니 앱 프로젝트를 처음부터 시작할 수도 있지만, 이 스타터를 사용하면 더 빠르고 원활한 개발 경험을 할 수 있습니다.

또한 미리 정의된 디자인 가이드를 따르므로 UI/UX의 일관성을 유지하는 데 도움이 됩니다.

이 프로젝트는 **Next.js**로 구축되었습니다. 다른 프레임워크를 사용할 계획이라도, 이 저장소는 `dapp-portal-sdk` 통합에 유용한 참고 자료가 될 수 있습니다.<br>

## 유니파이 앱 스타터 환경 시작 방법

유니파이 앱 스타터는 실행에 **Node.js**가 필요합니다. 패키지 관리자로 `pnpm`을 사용합니다(`npm`과 호환됨).

* 권장 Node.js 버전: **&gt;= 20.0.0**
* `.nvmrc`에 지정된 버전: **v20.18.0**
* 이전 버전도 부분적으로 작동할 수 있으나, Netlify 배포 도구와의 호환성을 위해 Node.js &gt;= 20.0.0이 필요합니다.

\*팁: Node 버전을 쉽게 관리하려면 [`nvm`](https://github.com/nvm-sh/nvm)을 사용하세요.

### 소스 코드 다운로드 및 실행

GitHub에서 저장소를 클론하거나 포크할 수 있습니다:\
[ https://github.com/techreadiness/unifi-apps-starter](https://github.com/techreadiness/unifi-apps-starter)

로컬에서 프로젝트를 실행하려면 저장소의 `README.md`에 있는 지침을 따르세요.

### 서버에 배포하기

Unifi Apps Starter를 로컬에서 실행하고 정상 작동하는지 확인한 후, **Netlify**를 사용하여 라이브 서버에 배포할 수 있습니다:

<details>

<summary>Netlify 계정이 필요합니다 </summary>

[Netlify (새 창 열기)](https://www.netlify.com/)는 정적 사이트 호스팅 서비스입니다. Netlify에 배포하기 전에 계정을 생성하세요. 본 페이지의 콘텐츠는 Netlify 무료 플랜에서 실행 가능합니다.

</details>```bash
# 루트 디렉토리로 이동
cd ./
# 프로젝트 빌드
pnpm build 
# 드래프트(미리보기) 환경에 배포
netlify deploy
# 검증 후 프로덕션 환경에 배포
netlify deploy --prod 
```

## Unifi Apps 스타터의 주요 기능

Unifi Apps 스타터는 기본적으로 구현된 여러 핵심 기능을 제공합니다.\
이는 `dapp-portal-sdk`의 핵심 기능 활용 방법을 보여주는 예시이며, **참조용 코드**로 활용해야 하며 최종 솔루션으로 간주해서는 안 됩니다.

### 지갑 연결/연결 해제

지갑 연결 및 연결 해제는 SDK 사용 시 가장 기본적인 기능입니다.\
코드에서 `walletProvider` 및 그 메서드 사용법을 확인할 수 있습니다.

### 암호화폐/법정화폐 결제

템플릿은 `paymentProvider`를 사용해 **암호화폐** 및 **법정화폐** 결제를 처리하는 방법을 보여줍니다.

다음과 같은 예시를 확인할 수 있습니다:

* 결제 ID 생성
* 결제 상태 확인
* 결제 완료

### KAIA/STRIPE 환율

결제를 지원하려면 미니 앱에서 **암호화폐(KAIA)**와 **법정화폐(STRIPE)** 간 적절한 가격 변환 로직을 적용해야 합니다.\
스타터에는 참고용으로 `usd-to-kaia` 함수가 포함되어 있습니다.

### LIFF 통합

**LINE 프론트엔드 프레임워크(LIFF)** 통합을 계획 중이라면, 본 프로젝트에는 다음과 같은 유용한 예시가 포함되어 있습니다:

* LIFF 초기화 시점
* `shareTargetPicker`와 같은 메서드 사용 방법
