# 유니피 마이그레이션 가이드

## 지갑 기능 업데이트

#### 시행일: 개별 통보 예정

개발자 여러분께,

본 공지는 Dapp Portal이 유니피(Unifi)로 리브랜딩될 예정임을 알리기 위함입니다.

리브랜딩과 함께 지갑 기능이 업데이트되며, 앱의 원활한 운영을 위해 일부 조치가 필요합니다.

#### 유니피 리브랜딩 개념

<table><thead><tr><th width="166.141357421875">현행 유지</th><th width="166.203857421875">변경 후</th><th>참고</th></tr></thead><tbody><tr><td>Dapp Portal</td><td>Unifi</td><td></td></tr><tr><td>미니 Dapp</td><td>유니피 앱</td><td></td></tr><tr><td>미니 Dapp SDK</td><td>유니피 앱 SDK</td><td>SDK 라이브러리 이름 변경<br>없음(~/@linenext/dapp-portal-sdk)</td></tr><tr><td>Dapp Portal Wallet</td><td>유니피 지갑</td><td></td></tr></tbody></table>## 유니피 개요

유니피는 카이아 블록체인 기반의 스테이블코인 지갑입니다.

사용자 등록 및 승인 권한 부여 후 자동 입금 서비스를 제공합니다.

* 출시 시 자동 입금 대상: USDT
* 기타 자산(예: KAIA, BORA)은 지원되나 자동 입금 대상에서 제외됩니다.

Dapp Portal 사용자가 Unifi로 마이그레이션 시:

* 사용자의 온체인 USDT 잔액이 0으로 표시될 수 있음
* 모든 USDT는 자동으로 Unifi 계정 풀로 입금됨

개발자는 온체인 잔액이 아닌 Unifi 계정 잔액을 반드시 조회해야 합니다. 따라서 USDT를 사용하는 개발자는 아래 단계를 따라야 합니다.

## SDK 버전 업데이트 필수

Unifi를 지원하는 새 SDK 버전은 **v1.5.2**입니다. SDK를 이 버전으로 업데이트하십시오.

업데이트하지 않을 경우:

* PaymentProvider를 통한 USDT 결제가 잔액 부족으로 실패합니다
* 자동 입금된 USDT가 감지되지 않습니다

Unifi 호환 SDK가 제공되는 즉시 업데이트하십시오.

#### 참고

PaymentProvider를 사용하면 SDK 버전만 업데이트하면 수정 없이 Unifi 계정에 자동 예치된 잔액으로 USDT 결제를 실행할 수 있습니다.

기타 기능은 Unifi Apps SDK와의 호환성을 보장하므로 변경이 필요하지 않습니다.

## 업데이트된 USDT 잔액 조회 방법

* 기존 방식: 온체인 USDT만 조회

`getErc20TokenBalance()`

* 변경 후: 온체인 + 유니피 예치 잔액 조회

`getErc20TokenBalanceWithDepositedBalance()`

## 스마트 계약 기반 USDT 전송 변경 사항

스왑을 포함한 스마트 계약을 통해 구현된 USDT 전송의 경우, 개발자는 `kaia_sendTransaction` 요청에 `depositTokenAddress` 및 `depositAmount`를 반드시 포함해야 합니다.

walletType이 WEB 또는 LIFF인 경우 변경이 필요합니다. walletType이 OKX 또는 BITGET인 경우 개발자는 기존 매개변수를 그대로 사용할 수 있습니다.

* 기존 매개변수

```
params = {
typeInt: 48,
from: &quot;0x4b53..dbe6&quot;,
to: &quot;contractAddress&quot;,
input: &quot;0xabcd...&quot;,
value: &quot;0x0&quot;
}
```

* 변경 후

```
params = {
typeInt: 48,
from: &quot;0x4b53..dbe6&quot;,
to: &quot;contractAddress&quot;,
input: &quot;0xabcd...&quot;,
depositTokenAddress: &quot;0xd077...&quot;, // USDT 계약 주소
depositAmount: &quot;100&quot;, // 전송할 USDT 금액
value: &quot;0x0&quot; // Kaia 금액
}
```

## Unifi용 연결 버튼 수정

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>{% file src=&quot;../.gitbook/assets/Unifi_Symbol_400x400.svg&quot; %}

{% file src=&quot;../.gitbook/assets/Unifi_Symbol_400x400.png&quot; %}
