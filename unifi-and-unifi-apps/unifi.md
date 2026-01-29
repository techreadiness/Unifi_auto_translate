---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/unifi-and-unifi-apps/unifi-migration-guide
---

# Unifi 마이그레이션 가이드

## 월렛 기능 업데이트 안내

#### 적용 일시: 추후 개별 안내

안녕하세요,

Dapp Portal이 Unifi로 새롭게 리브랜딩될 예정임을 안내해 드립니다. 이번 리브랜딩과 함께 월렛(Wallet) 기능 업데이트가 진행될 예정이며, 귀사의 앱이 문제없이 원활하게 운영될 수 있도록 필수적인 조치가 필요합니다.

#### Unifi 리브랜딩 개요

<table><thead><tr><th width="166.141357421875">변경 전 (AS-IS)</th><th width="166.203857421875">변경 후 (TO-BE)</th><th>비고 (NOTE)</th></tr></thead><tbody><tr><td>Dapp Portal</td><td>Unifi</td><td></td></tr><tr><td>Mini Dapp</td><td>Unifi Apps</td><td></td></tr><tr><td>Mini Dapp SDK</td><td>Unifi Apps SDK</td><td>SDK 라이브러리 이름은 변경되지 않습니다.<br>(~/@linenext/dapp-portal-sdk)</td></tr><tr><td>Dapp Portal Wallet</td><td>Unifi Wallet</td><td></td></tr></tbody></table>

## Unifi 개요

Unifi는 Kaia 블록체인을 기반으로 구축된 스테이블코인 월렛입니다. 사용자 등록 및 승인(Approve) 권한 부여 후, 자동 예치(Auto-deposit) 서비스를 제공합니다.

* 런칭 시 자동 예치 대상: USDT
* 기타 자산(예: KAIA, BORA): 계속 지원되지만 자동 예치 대상에는 포함되지 않습니다.

Dapp Portal 사용자가 Unifi로 마이그레이션하면 다음과 같은 사항이 적용됩니다:

* 사용자의 온체인 USDT 잔액이 0으로 표시될 수 있습니다.
* 모든 USDT는 Unifi의 계정 풀(Account Pool)로 자동 예치됩니다.

개발자는 온체인 잔액뿐만 아니라 Unifi 계정 잔액을 함께 조회해야 합니다. 따라서 USDT를 사용하는 개발자는 반드시 아래 절차를 따라야 합니다.

## SDK 버전 업데이트 필수

Unifi를 지원하는 새로운 SDK 버전은 v1.5.2입니다. SDK를 해당 버전으로 업데이트해 주세요.

업데이트하지 않을 경우:

* 잔액 부족으로 인해 PaymentProvider를 통한 USDT 결제가 실패하게 됩니다.
* 자동 예치된 USDT를 감지할 수 없습니다.

Unifi 호환 SDK가 배포되는 즉시 업데이트해 주시기 바랍니다.

#### 참고

PaymentProvider를 사용하는 경우, 별도의 코드 수정 없이 SDK 버전만 업데이트하면 Unifi 계정에 자동 예치된 잔액을 사용하여 USDT 결제를 실행할 수 있습니다. 그 외 기능은 Unifi Apps SDK와의 호환성이 보장되므로 변경이 필요하지 않습니다.

## 변경된 USDT 잔액 조회 방식

* AS-IS (기존): 온체인 USDT만 조회

`getErc20TokenBalance()`

* TO-BE (변경 후): 온체인 + Unifi 예치 잔액 조회

`getErc20TokenBalanceWithDepositedBalance()`

## 스마트 컨트랙트 기반 USDT 전송 변경 사항

스마트 컨트랙트(Swap 포함)를 통해 구현된 USDT 전송의 경우, 개발자는 `kaia_sendTransaction` 요청에 `depositTokenAddress`와 `depositAmount` 파라미터를 포함해야 합니다.

* 이 변경 사항은 `walletType`이 WEB 또는 LIFF인 경우에만 필요합니다.
* `walletType`이 OKX 또는 BITGET인 경우, 개발자는 기존(AS-IS) 파라미터를 그대로 사용할 수 있습니다.



* AS-IS (기존)

```
params = {
typeInt: 48,
from: "0x4b53..dbe6",
to: "contractAddress",
input: "0xabcd...",
value: "0x0"
}
```

* TO-BE (변경 후)

```
params = {
typeInt: 48,
from: "0x4b53..dbe6",
to: "contractAddress",
input: "0xabcd...",
depositTokenAddress: "0xd077...", // USDT contract address
depositAmount: "100", // Amount of USDT to transfer
value: "0x0" // Kaia Amount
}
```

Unifi용 연결(Connect) 버튼 수정

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

{% file src="../.gitbook/assets/Unifi_Symbol_400x400.svg" %}

{% file src="../.gitbook/assets/Unifi_Symbol_400x400.png" %}
