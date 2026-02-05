---
hidden: true
metaLinks:
  alternates:
    - https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/unifi-apps
---

# 유니피 앱

## 유니피 앱 구축 방법

<div data-full-width="true"><figure><img src="../.gitbook/assets/development_flow.png" alt=""><figcaption></figcaption></figure></div>

이 가이드는 LINE 및 웹 환경에 유니파이 앱을 배포하기 위한 필수 통합 아키텍처와 순차적 단계를 설명합니다.

\
지원할 특정 플랫폼 또는 통합 유형에 따라 각 단계를 따르십시오.

### ① LINE 버전 개발 — LIFF SDK 통합

유니파이 앱은 두 가지 방식으로 LINE 기반 경험을 제공할 수 있습니다:

* LINE 미니 앱
* LINE 로그인 LIFF

둘 다 LINE 모바일 앱 내에서 실행되며 **LIFF SDK**를 사용하여 구현되지만, 서로 다른 채널 유형을 사용하고 별도의 트랙을 통해 온보딩됩니다.

#### 주요 차이점

| 항목                 | LINE 미니 앱                                                              | LINE 로그인 LIFF                                                                              |
| -------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| 채널              | LINE 미니 앱 채널                                                      | LINE 로그인 채널                                                                           |
| 앱 스토어 정책     | 앱 스토어 정책 준수                                                                 | -                                                                                            |
| LIFF SDK 사용       | 예                                                                        | 예                                                                                          |
| Unifi Apps SDK 사용 | <ul><li>예</li><li>WalletProvider</li><li>결제 제공자(IAP)</li></ul> | <ul><li>예</li><li>WalletProvider</li><li>결제 제공자<br>(암호화폐/Stripe 법정화폐)</li></ul> |

📌 자세한 지침은 [**LINE 통합**](../mini-dapp/line-integration/) 문서를 참조하세요.\
📌 LINE MINI 앱과 LINE 로그인 LIFF는 기술적으로 Unifi Apps SDK를 기본 웹 서비스에 먼저 통합한 후, 그 위에 LIFF SDK를 추가하는 방식으로 구현됩니다.\
따라서 기술적 관점에서 웹 및 Unifi Apps SDK 환경은 본질적으로 포함됩니다.

### ② 웹 버전 개발

비(非) LINE 사용자를 위한 **웹 브라우저 버전** 개발을 **권장**합니다.

다음 기능을 지원하려면 웹 버전에 **Unifi Apps SDK를 반드시 통합**해야 합니다:

* **WalletProvider**
* **PaymentProvider (암호화폐 / Stripe 법정화폐)**

### ③ Web3 통합 (WalletProvider)

Unifi Apps SDK는 계정 생성 및 소유권 확인과 같은 지갑 기능을 지원합니다.

| 버전         | 지원되는 지갑 유형                                                                     |
| --------------- | ------------------------------------------------------------------------------------------ |
| LINE MINI 앱   | <ul><li>LINE (Liff)</li><li>OKX, Bitget Wallet</li></ul>                                   |
| LINE 로그인 LIFF | <ul><li>LINE (Liff)</li><li>OKX, Bitget 지갑</li></ul>                                   |
| 웹             | <ul><li>소셜 로그인 (웹)</li><li>Kaia 지갑 앱/확장 프로그램, OKX, Bitget 지갑</li></ul> |

📌 자세한 지침은 [**지갑 제공업체**](../mini-dapp/mini-dapp-sdk/wallet/) 문서를 참조하세요.

### ④ 결제 통합 (PaymentProvider)

수익화를 지원하기 위해 모든 Unifi 앱은 **앱 내 아이템 구매 기능을 반드시 제공해야** 합니다.

| 버전         | 지원 결제 수단       |
| --------------- | ------------------------------- |
| LINE MINI 앱   | IAP 결제                    |
| LINE 로그인 LIFF | 암호화폐 및 Stripe(법정화폐) 결제 |
| 웹             | 암호화폐 및 Stripe(법정화폐) 결제 |

📌 자세한 지침은 [결제 제공자](../mini-dapp/mini-dapp-sdk/payment/) 문서를 참조하세요.

### ⑤ 앱 심사 — 품질 및 규정 준수 점검

제출 및 심사 제공자는 버전에 따라 다릅니다:

<table><thead><tr><th width="166.32421875">버전</th><th>데모 제출/검토 권한</th></tr></thead><tbody><tr><td>LINE MINI 앱</td><td><ul><li>LINE NEXT (사전 검토)</li><li>LY (최종 승인)</li><li><strong>LINE NEXT 검토 완료 후</strong> LY 제출 필수</li></ul></td></tr><tr><td>LINE 로그인 LIFF</td><td><ul><li>LINE NEXT</li><li>이메일 제출</li></ul></td></tr><tr><td>웹</td><td><ul><li>LINE NEXT</li><li>이메일 제출</li></ul></td></tr></tbody></table>⑥ 온보딩 및 출시

<table><thead><tr><th width="160.8515625">버전</th><th>추천 배치</th><th>노출 영역</th><th>서비스 제공 사용자</th></tr></thead><tbody><tr><td>LINE MINI 앱</td><td>LINE 앱 &amp; Unifi</td><td><ul><li>LINE 앱 내 MINI 탭</li><li>Unifi 내 앱</li></ul></td><td>일본 LINE 사용자</td></tr><tr><td>LINE 로그인 LIFF</td><td>Unifi</td><td>Unifi의 앱</td><td>글로벌 LINE 사용자</td></tr><tr><td>웹</td><td>Unifi</td><td>Unifi의 앱</td><td>글로벌 사용자</td></tr></tbody></table>또한 별도의 트랙을 통해 정보를 등록하면 유니피에 소개될 수 있으며 NFT를 판매할 수도 있습니다.
