# Reown을 통한 도메인 검증

## 미니 Dapp SDK로 Bitget 지갑 사용 방법

<figure><img src="../../../.gitbook/assets/스크린샷 2025-07-16 오후 4.52.11.png" alt=""><figcaption><p>흐름도 </p></figcaption></figure>미니 Dapp SDK는 WalletConnect를 통해 Bitget 지갑을 제공합니다. 미니 Dapp SDK로 Bitget 지갑을 제공하려면 WalletConnect에서 요구하는 도메인 인증을 사전에 완료해야 합니다.

아래 가이드에 따라 도메인 인증을 완료하고 Reown에서 생성된 `ProjectId`를 Dapp Portal 팀과 공유해 주세요.

:exclamation:<mark style="color:red;">**Bitget 연동을 지원하는 SDK 버전으로 업그레이드하더라도, 도메인 등록 및 ProjectId 제출이 완료되지 않으면 Bitget 지갑을 사용할 수 없습니다.**</mark>



## Reown 대시보드를 통한 도메인 추가 가이드

### 참고 자료

* [https://dashboard.reown.com/](https://dashboard.reown.com/)
* [https://docs.reown.com/cloud/relay](https://docs.reown.com/cloud/relay)
* 도메인은 프로토콜 포함 전체(`http://` | `https://`)로 등록해야 합니다.
* 레코드 등록 시 도메인 끝에 슬래시(/)가 포함되지 않도록 하십시오.
  * <mark style="color:blue;">올바른 예</mark>

: https://dappportal.io
  * <mark style="color:red;">잘못된 예</mark>

: https://dappportal.io/

### 1.  Reown 대시보드 접속 및 검증 시작

* 대시보드에서 Reown 계정에 로그인하세요. ([https://dashboard.reown.com/](https://dashboard.reown.com/))
* 도메인 탭으로 이동
* 허용 목록에 추가할 도메인 입력

### 2. Dapp Portal 팀에 ProjectId 제출

* 검증 후 `ProjectId`를 제출하여 Mini Dapp SDK에 추가하세요.
* 텔레그램: <mark style="color:blue;">**@dappportal\_official**</mark>

* 다른 경로로 기술 지원 채널을 이용 중이라면 해당 채널을 통해 `ProjectId`를 공유할 수 있습니다.
