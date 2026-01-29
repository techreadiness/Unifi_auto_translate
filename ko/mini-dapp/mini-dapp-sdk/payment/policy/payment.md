# 결제

## 결제 방법

<figure><img src="../../../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

* <mark style="color:red;">**미니 Dapp은 제품 구매 화면에서 법정화폐와 암호화폐 결제 옵션을 모두 제공해야 하며, 각 결제 버튼은 별도로 표시되어야 합니다.**</mark>

### a. 법정화폐

결제 수단으로는 신용/체크카드(VISA, MasterCard, AMEX, JCB 등 주요 브랜드), Apple Pay, Google Play, 네이버페이(원화 전용), 카카오페이(원화 전용)를 지원합니다.

* 결제 수단은 연결된 기기의 OS 및 결제 통화에 따라 동적으로 자동 변경됩니다.
* 결제 처리업체 정책에 따라 향후 결제 수단이 변경될 수 있습니다.
* LINE IAP 결제는 곧 지원될 예정입니다.

미니 앱의 LIFF 및 웹 버전 모두에서 법정화폐 결제를 지원합니다.

### b. 암호화폐

결제 수단으로 KAIA와 USDT를 지원합니다.

미니 앱의 LIFF 및 웹 버전 모두에서 암호화폐 결제를 지원합니다.

## 지원 통화

<table><thead><tr><th>유형</th><th width="146">통화</th><th width="139">소수점(최대)</th><th>최대 청구액</th><th>최소 청구 금액</th></tr></thead><tbody><tr><td>피아트</td><td>USD</td><td>2</td><td>999,999</td><td>0.50</td></tr><tr><td></td><td>KRW</td><td>0</td><td>999,999</td><td>750</td></tr><tr><td></td><td>JPY</td><td>0</td><td>999,999</td><td>80</td></tr><tr><td></td><td>TWD(NTD)</td><td>2</td><td>999,999</td><td>17</td></tr><tr><td></td><td>THB</td><td>2</td><td>999,999</td><td>18</td></tr><tr><td>암호화폐</td><td>KAIA</td><td>4</td><td>999,999</td><td>0.01</td></tr><tr><td></td><td>USDT</td><td>2</td><td>999,999</td><td>0.01</td></tr></tbody></table>

## 제품 가격

* **미니 Dapp SDK를 통해 판매되는 제품의 가격은 법정화폐와 암호화폐로 모두 표시되어야 하며, 일정한 안정성을 유지해야 합니다.**
  * 이는 Web2 및 Web3 사용자 모두에게 안정적인 구매 경험을 제공하고, 과도한 가격 변동으로 인한 혼란을 방지하며, Web2와 Web3 사용자의 요구를 균형 있게 반영하기 위함입니다. 이를 통해 모든 사용자에게 이해하기 쉽고 신뢰할 수 있으며 안정적인 구매 환경을 조성하고자 합니다.
* USD(미국 달러)가 기본 결제 통화입니다.
* 각 미니 앱은 필요 시 사용자의 국가 정보에 기반하여 추가 현지 통화(JPY, TWD, THB, KRW)를 선택적으로 지원할 수 있습니다.

| 사용자 국가 (브라우저 언어 기준) | 사용자에게 표시되는 제품 가격 통화                                        |
| --------------------------------------- | ------------------------------------------------------------------------------ |
| 일본                                   | <ul><li>기본값 : USD, KAIA, USDT</li><li>선택적 : JPY, KAIA, USDT</li></ul> |
| 태국                                | <ul><li>기본 : USD, KAIA, USDT</li><li>선택 가능 : THB, KAIA, USDT</li></ul> |
| 대만                                  | <ul><li>기본값 : USD, KAIA, USDT</li><li>선택 가능 : TWD, KAIA, USDT</li></ul> |
| 대한민국                             | <ul><li>기본값 : USD, KAIA, USDT</li><li>선택 가능 : KRW, KAIA, USDT</li></ul> |
| 기타 국가                             | <ul><li>기본값 : USD, KAIA, USDT</li></ul>                                    |

### 결제 요청 시 입력할 상품 가격

* 사용자가 법정화폐 결제를 선택할 경우, 미니 앱 운영자는 USD 기준 고정 금액을 입력하여 결제를 요청해야 합니다.
* 사용자가 암호화폐 결제를 선택할 경우, 미니 앱 운영자는 $KAIA 기준 고정 금액을 입력하여 결제를 요청해야 합니다.

### 명확한 알림 제공

* <mark style="color:red;">**중복 결제나 잘못된 결제 같은 오류를 최소화하기 위해, Dapp은 사용자가 성공 및 실패/취소된 구매 결과를 &quot;명확하고&quot; &quot;직관적인&quot; 방식으로 인식할 수 있도록 즉시 적절한 알림 메시지를 제공해야 합니다**</mark>

<table><thead><tr><th width="167">이벤트</th><th>설명</th><th>사용자에게 알릴 정보 (예시)</th></tr></thead><tbody><tr><td>구매 성공</td><td>법정화폐/암호화폐 결제 성공 및 아이템 배송 완료</td><td>구매 성공</td></tr><tr><td>구매 실패/취소됨</td><td>사용자가 법정화폐/암호화폐 결제를 요청했으나 결제 실패</td><td>구매 실패</td></tr><tr><td></td><td>사용자가 피아트/암호화폐 결제 화면에서 &quot;뒤로&quot; 버튼을 클릭하거나 화면을 종료함</td><td>구매 취소됨</td></tr><tr><td></td><td>사용자가 암호화폐 결제 화면에서 서명 거절 버튼을 클릭함</td><td>구매 취소됨</td></tr><tr><td></td><td>사용자의 암호화폐 잔액이 부족합니다</td><td>잔액 부족</td></tr><tr><td></td><td>기타 오류</td><td>나중에 다시 시도해 주세요</td></tr></tbody></table>### 결제 내역

**SDK 문서를 참조하여 적절한 위치에 사용자에게 결제 내역을 제공하십시오.**

<figure><img src="../../../../.gitbook/assets/minimum (3).png" alt=""><figcaption></figcaption></figure>
