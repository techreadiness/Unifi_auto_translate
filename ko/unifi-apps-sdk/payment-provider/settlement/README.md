# 정산

**본 문서의 내용은 향후 상황 또는 정책 변경에 따라 변경될 수 있습니다.**

본 가이드는 유니피가 제공하는 결제 시스템에 대한 개요를 제공합니다. \
결제 정책, 환불 정책, 정산 정책에 대한 상세 정보를 포함합니다.

## 현금 흐름

* 상품 가격: 상품 판매 금액
* 플랫폼 수수료(서비스 수수료): 플랫폼 제공에 대해 LINE NEXT가 받는 수수료.
* 로열티 수수료(콘텐츠 수수료): Unifi 앱이 NFT C2C 거래에 대한 로열티로 받는 수수료.
* 결제 솔루션 수수료: 결제 솔루션 제공을 위해 결제 프로세서가 징수하는 수수료.

## 유니파이 앱 내 아이템

### 1-1. 법정화폐 결제 (B2C)

지급액: 제품 가격 - 플랫폼 수수료 - 결제 솔루션 수수료 - 기타 모든 비용\*

* 기타 모든 비용: OTC 전환 수수료 등.

<figure><img src="../../../.gitbook/assets/Fiat Payment.png" alt=""><figcaption></figcaption></figure>### 1-2. 법정화폐 정산

#### a. 정산 통화

정산 자금은 Kaia 블록체인을 기반으로 USDT로 지급됩니다.

#### b. 정산 주기

월간 정산 (N월에 발생한 거래에 대한 정산 자금 지급은 N+1일에 이루어짐)

#### c. 정산 절차

* 결제 처리사가 거래 수수료를 공제하고 결제 금액을 확정 후 LINE NEXT에 지급 (N+1 주 1~2).
* LINE NEXT가 플랫폼 수수료를 공제하고 잔액을 USDT로 전환 (N+1 주 3).
* 관련 비용 전액 공제 후, Unifi Apps는 결제 보고서를 통해 최종 결제 금액을 확인하고 직접 청구하여 지급받음 (N+1 주 4).

#### d. 예시

3월 결제 건 기준

* 4월 W1\~W2: 결제 대행사가 결제 수수료를 공제하고 최종 정산 금액을 확정하여 LINE NEXT로 송금
* 4월 W3: LINE NEXT가 플랫폼 수수료를 공제하고 잔여 금액을 암호화폐로 전환
* 4월 W4: 유니파이 앱은 정산 보고서에서 최종 정산 금액을 확인하고 직접 청구하여 지급받을 수 있습니다.

#### e. 법정화폐 정산 정보

<table><thead><tr><th width="208.62353515625">정보</th><th>설명</th></tr></thead><tbody><tr><td>결제 통화</td><td><a href="https://kaiascan.io/token/0xd077a400968890eacc75cdc901f0356c943e4fdb?tabId=tokenTransfer&#x26;page=1">USDT</a> (카이아 블록체인 기반 USD 페그 스테이블코인)</td></tr><tr><td>지급 주기</td><td>월간 (N월에 지급 -&gt; N+1월에 청구)</td></tr><tr><td>결제 운영사</td><td>Unifi Apps에서 직접 청구 가능</td></tr><tr><td>청구 방법</td><td><p>2025년 7월 말 예정된 4월~6월 STRIPE 수익 정산부터 다음 시스템이 적용됩니다. 7월 수익 정산 이후에도 동일한 월별 정산 구조가 지속됩니다.</p><p></p><ol><li><p><a href="../../../mini-dapp/mini-dapp-sdk/payment/policy/how-to-claim-usdt-for-stripe-transaction.md"><strong>제공된 가이드</strong></a><strong>에 따라 청구 API를 직접 호출</strong></p><ol><li>청구 API 사용법은 유니피 앱스 문서에 사전에 게시될 예정입니다.</li><li>이는 7월 말에 진행될 4월~6월 피아트 수익 정산부터 적용되며, 8월부터는 매월 동일한 절차로 정산이 진행됩니다.</li><li>향후 전용 청구 페이지도 제공되어 직접 API 통합 없이도 간편하게 청구가 가능할 예정입니다.</li></ol></li><li><strong>수익 정산을 위해 USDT는 Unifi Apps 지정 지갑 주소로 온체인 전송됩니다.</strong></li></ol></td></tr><tr><td>청구 가능 주소</td><td>온보딩 계약상의 주소.<br>(암호화폐 정산용 주소와 동일)</td></tr><tr><td>인출 마감일</td><td>인출 기간이 시작되면 Unifi Apps는 자유롭게 인출할 수 있습니다.</td></tr></tbody></table>### 2-1. 암호화폐 결제 (B2C)

지급액: 제품 가격 - 플랫폼 수수료

<figure><img src="../../../.gitbook/assets/Crypto Payment(B2C) (1).png" alt=""><figcaption></figcaption></figure>### 2-2. 암호화폐 정산

#### a. 정산 통화

정산 자금은 암호화폐로 지급됩니다.

#### b. 정산 주기

실시간 정산

#### c. 정산 절차

* 스마트 계약이 상품 가격을 기반으로 관련 수수료 금액을 자동 계산하여 잔액을 판매자에게 지급합니다.
* LINE NEXT는 분기별 정산 보고서(N+3일차)를 제공합니다.

## NFT

### 1. 암호화폐 결제 (B2C)

지급액: 상품 가격 - 플랫폼 수수료

* 플랫폼 수수료: 프로모션 기간 중 할인된 수수료율이 적용됩니다.

<figure><img src="../../../.gitbook/assets/Crypto Payment(B2C) (2).png" alt=""><figcaption></figcaption></figure>### 2. 암호화폐 결제 (C2C)

지급액: 로열티 수수료\*

* 제품 가격의 0~10% 범위 내에서 유니파이 앱이 직접 설정합니다.

<figure><img src="../../../.gitbook/assets/Crypto Payment(C2C).png" alt=""><figcaption></figcaption></figure>### 3. NFT 암호화폐 정산

유니파이 앱 내 아이템과 동일하게 즉시 정산됩니다.
