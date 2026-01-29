# Dapp 스타터

Dapp 개발을 처음 접할 때는 어디서부터 시작해야 할지 막막할 수 있습니다. 이런 경우 **Dapp 스타터**가 유용한 출발점이 될 수 있습니다.

Dapp 스타터는 Dapp 구축에 필요한 핵심 기능을 포함하는 템플릿입니다. 이 템플릿을 기반으로 자신만의 Dapp을 커스터마이징하고 구축할 수 있습니다.
이 가이드는 다음 단계로 Dapp 스타터를 안내합니다:



* [Dapp 스타터란 무엇인가요?](dapp-starter.md#what-is-the-dapp-starter)
* [Dapp 스타터 시작 방법](dapp-starter.md#how-to-get-started-with-the-dap-starter)
  * 환경 설정
  * 소스 코드 다운로드 및 실행
  * 서버에 배포하기
* [Dapp Starter의 주요 기능](dapp-starter.md#key-features-of-thedapp-starter)
  * 지갑 연결/분리
  * 암호화폐/법정화폐 결제
  * KAIA/STRIPE 환율 변환
  * LIFF 통합##<br>

Dapp Starter란 무엇인가요?

**Dapp Starter**는 `dapp-portal-sdk`를 쉽게 통합할 수 있도록 설계된 템플릿 프로젝트입니다. Dapp 프로젝트를 처음부터 시작할 수도 있지만, 이 스타터를 사용하면 더 빠르고 원활한 개발 경험을 할 수 있습니다.

또한 미리 정의된 디자인 가이드를 따르므로 UI/UX의 일관성을 유지하는 데 도움이 됩니다.

이 프로젝트는 **Next.js**로 구축되었습니다. 다른 프레임워크를 사용할 계획이라도, 이 저장소는 `dapp-portal-sdk` 통합에 유용한 참고 자료로 활용될 수 있습니다.<br>

## Dapp 스타터 시작 방법

###  환경

Dapp 스타터는 실행에 **Node.js**가 필요합니다. 패키지 관리자로 `pnpm`을 사용합니다(`npm`과 호환됨).

* 권장 Node.js 버전: **&gt;= 20.0.0**
* `.nvmrc`에 지정된 버전: **v20.18.0**
* 이전 버전도 부분적으로 작동할 수 있으나, Netlify 배포 도구와의 호환성을 위해 Node.js &gt;= 20.0.0이 필요합니다.

\*팁: Node 버전을 쉽게 관리하려면 [`nvm`](https://github.com/nvm-sh/nvm)을 사용하세요.

### 소스 코드 다운로드 및 실행

GitHub에서 저장소를 클론하거나 포크할 수 있습니다:\
 [https://github.com/techreadiness/dapp-starter](https://github.com/techreadiness/dapp-starter)

로컬에서 프로젝트를 실행하려면 저장소의 `README.md`에 있는 지침을 따르세요.

### 서버에 배포하기

Dapp Starter를 로컬에서 실행하고 정상 작동하는지 확인한 후, **Netlify**를 사용하여 라이브 서버에 배포할 수 있습니다:

<details>

<summary>Netlify 계정이 필요합니다 </summary>

[Netlify (새 창 열기)](https://www.netlify.com/)는 정적 사이트 호스팅 서비스입니다. Netlify에 배포하기 전에 계정을 생성하세요. 본 페이지의 콘텐츠는 Netlify 무료 플랜에서 실행 가능합니다.

</details>

<details>

<summary>.env.production 파일은 Netlify 설정에서 저장해야 합니다.</summary>

프로젝트 &gt; 프로젝트 구성 &gt; 환경 변수로 이동하여 .env.production 변수를 저장하세요. 

</details>```bash
# 루트 디렉토리로 이동
cd ./
# 프로젝트 빌드
npm build 
# netlify cli 설치
npm install -g netlify-cli
# Netlify 로그인 및 저장소 연결
netlify login
# 드래프트(미리보기) 환경에 배포
netlify deploy
# 검증 후 프로덕션 환경에 배포
netlify deploy --prod 
```

공식 게시 버전은 [https://dapp-starter.netlify.app](https://dapp-starter.netlify.app)에서 확인할 수 있습니다.

## Dapp 스타터의 주요 기능

Dapp 스타터는 기본적으로 구현된 여러 핵심 기능을 제공합니다.
이들은 `dapp-portal-sdk`의 핵심 기능 사용법을 보여주는 예시이지만, **참조용 코드**로만 활용해야 하며 최종 솔루션으로 간주해서는 안 됩니다.

### 지갑 연결/해제

지갑 연결 및 해제는 SDK 사용 시 가장 기본적인 기능입니다.\
코드 내에서 `walletProvider` 및 관련 메서드 사용법을 확인할 수 있습니다.<br>

**참조용 코드**\
[지갑 연결 및 연결 해제 관련 함수](https://github.com/techreadiness/dapp-starter/blob/cf5227243e2d878effdc634cd83f27b75b5b65e5/src/components/Wallet/Sdk/walletSdk.hooks.ts#L58)

### 지갑 세션 지속성

사용자가 한 번 로그인한 후 편의상 지갑 세션이 활성 상태로 유지되도록, 먼저\
`walletProvider.request({ method: &#x27;kaia_accounts&#x27; })`를 호출하여 로그인 세션이 존재하는지 확인할 수 있습니다.<br>

**참고 코드**\
[kaia_accounts를 이용한 세션 유지](https://github.com/techreadiness/dapp-starter/blob/cf5227243e2d878effdc634cd83f27b75b5b65e5/src/app/page.tsx#L15)

### 암호화폐/법정화폐 결제

이 템플릿은 `paymentProvider`를 사용하여 **암호화폐** 및 **법정화폐** 결제를 모두 처리하는 방법을 보여줍니다.

다음과 같은 예시를 확인할 수 있습니다:

* 결제 ID 생성
* 결제 상태 확인
* 결제<br>

완료**참고 코드**

[결제 관련 함수](https://github.com/techreadiness/dapp-starter/blob/cf5227243e2d878effdc634cd83f27b75b5b65e5/src/components/Store/Sdk/paymentSdk.hooks.ts#L39)

### KAIA/STRIPE 환율

결제를 지원하려면 Dapp에서 **암호화폐(KAIA)**와 **법정화폐(STRIPE)** 간 적절한 가격 변환 로직을 적용해야 합니다.\
스타터에는 참고용으로 `usd-to-kaia` 함수가 포함되어 있습니다.<br>

**참고 코드**\
[USD에서 KAIA로의 변환](https://github.com/techreadiness/dapp-starter/blob/cf5227243e2d878effdc634cd83f27b75b5b65e5/src/app/api/usd-to-kaia/route.ts#L3)

### KAIA/USDT 잔액

이 템플릿은 KAIA와 ERC20 기반 토큰의 잔액을 모두 조회하는 방법을 보여줍니다.\
\
**참고 코드**\
[카이아 잔액](https://github.com/techreadiness/dapp-starter/blob/cf5227243e2d878effdc634cd83f27b75b5b65e5/src/components/Wallet/Sdk/walletSdk.hooks.ts#L87)\
[erc20token 잔액](https://github.com/techreadiness/dapp-starter/blob/cf5227243e2d878effdc634cd83f27b75b5b65e5/src/components/Wallet/Sdk/walletSdk.hooks.ts#L100)

### LIFF 통합

**LINE 프론트엔드 프레임워크(LIFF)**와 통합할 계획이라면, 이 프로젝트에는 다음과 같은 유용한 예시가 포함되어 있습니다:

* LIFF 초기화 시점
* `shareTargetPicker`\
  <br>

**참조 코드**와 같은 메서드 사용 방법

[LIFF 초기화](https://github.com/techreadiness/dapp-starter/blob/cf5227243e2d878effdc634cd83f27b75b5b65e5/src/components/Wallet/Sdk/walletSdk.hooks.ts#L38)\
[shareTargetPicker 메서드](https://github.com/techreadiness/dapp-starter/blob/cf5227243e2d878effdc634cd83f27b75b5b65e5/src/components/Invitation/Invitation.hooks.ts#L4)
