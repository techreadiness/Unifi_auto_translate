# LINE MINI 앱

## LINE MINI 앱 온보딩 요건

* LINE MINI 앱 온보딩은 **일본 법인 번호를 보유한 기업** 또는 **일본 거주 개인 사업자**에게만 제공됩니다.
* MINI 앱 온보딩을 원하는 글로벌 빌더는 **LINE NEXT**와 별도로 절차를 협의해야 합니다.
* [LINE 미니 앱 정책 &gt;](https://terms2.line.me/LINE_MINI_App?lang=en)

{% stepper %}
{% step %}
## [LINE 비즈니스 ID 생성 및 LINE Developers 로그인](https://developers.line.biz/en/)

* 개인 LINE 계정 또는 이메일로 로그인
* LINE Developers Console 접근을 위한 비즈니스 ID 생성

<figure><img src="../../.gitbook/assets/LINE Business ID.png" alt="" width="240"><figcaption></figcaption></figure>{% endstep %}

{% step %}
## [개발자 정보 등록](https://developers.line.biz/en/docs/line-developers-console/login-account/#register-as-developer)

* 개발자 이름과 이메일 추가

<figure><img src="../../.gitbook/assets/developer information.png" alt="" width="375"><figcaption></figcaption></figure>{% endstep %}

{% step %}
## [제공자 생성](https://developers.line.biz/en/docs/liff/getting-started/#step-one-create-provider)

* **제공자 이름** 입력
* 제공자 생성
{% endstep %}

{% step %}
## [LINE MINI 앱 생성](https://developers.line.biz/en/docs/line-mini-app/discover/console-guide/)

⚠️ **LINE 미니 앱과 LINE 로그인 LIFF를 모두 배포하려면 동일한 LINE 제공자 아래에 두 채널을 생성하세요.**\
동일한 제공자 아래에 채널이 생성되면 사용자의 **LINE UID가 채널 간에 일관되게 유지**되어 안정적인 사용자 추적 및 분석이 가능합니다.

<figure><img src="../../.gitbook/assets/channel_MINI App.png" alt="" width="563"><figcaption></figcaption></figure>| 필드                         | 값                               |
| ----------------------------- | ----------------------------------- |
| 서비스 제공 지역 | 대상 서비스 국가 선택       |
| 채널 이름                  | 유니파이 앱스 이름 입력               |
| 채널 설명           | 간단한 서비스 설명 제공 |

<figure><img src="../../.gitbook/assets/create_mini app.png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
## 기본 설정

&gt; 위치: LINE Developers → 제공자 → LINE MINI 앱 채널 → 기본 설정

| 필드              | 값                                                                                                                                                                                            |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 채널 아이콘       | 130×130px 이미지 업로드                                                                                                                                                                         |
| 개인정보 처리방침 URL | <ul><li>Unifi Apps 개인정보처리방침 URL 입력</li><li>개인정보 처리방침 URL은 <strong>기업 </strong>도메인에 속해야 합니다.</li></ul>                                                         |
| 현지화       | <ul><li>최소 3개 언어 입력 (EN, JP 필수)</li><li>불명확하거나 모호한 현지화 콘텐츠는 자주 거부됩니다. 서비스 설명이 정확한지 확인하세요.</li></ul> |

<figure><img src="../../.gitbook/assets/basic settings_mini app.png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
## 웹 앱 설정

&gt; 위치: LINE Developers → 제공자 → LINE MINI 앱 채널 → 웹 앱 설정

| 필드             | 값                                                                                 |
| ----------------- | ------------------------------------------------------------------------------------- |
| 엔드포인트 URL      | <ul><li>Unifi Apps URL 입력</li><li>개발 / 검토 / 운영 URL</li></ul> |
| 스코프            | `openid` (필수), `profile` (선택)                                             |
| 친구 추가 옵션 | 켜기 (일반)                                                                           |

<figure><img src="../../.gitbook/assets/web app_mini app.png" alt=""><figcaption></figcaption></figure>{% endstep %}

{% step %}
## 비즈니스 정보

| 필드                           | 값                                                                                  |
| ------------------------------- | -------------------------------------------------------------------------------------- |
| 고객 지원 페이지 URL       | 고객 지원 문의 페이지                                                                        |
| 고객 지원 이메일 주소  | 고객 지원 이메일                                                                               |
| LINE 공식 계정 ID        | 11단계 이후 사용 가능                                                                |
| 서비스 회사명            | 법인 또는 사업자명                                                    |
| 서비스 회사 유형            | 법인 / 개인 사업자                                                              |
| 증명 서류            | 사업자등록증                                                      |
| 신분 증명 서류         | 대표자 신분증                                                                    |
| 웹사이트 URL                     | 공식 서비스 웹사이트                                                               |
| 이메일 주소                   | 법인 도메인 이메일                                                                 |
| 개발사 정보            | 서비스 소유자와 다른 경우 별도 입력 (또는 &quot;서비스 회사와 동일&quot; 선택) |

<figure><img src="../../.gitbook/assets/business_mini app.png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
## 연락처 정보

| 필드                  | 값                                                                                             |
| ---------------------- | ------------------------------------------------------------------------------------------------- |
| 이름 / 성 | 담당자                                                                                  |
| 이메일 주소          | 기업 도메인 이메일 (심사 결과 및 안내문 발송처)                               |
| 전화번호           | 담당자 연락처                                                              |
| 회사명           | 서비스 소유자 (법인)                                                                      |
| 회사 주소        | 등록 사업장 주소                                                                       |
| 등록 번호    | <ul><li>법인: 법인 번호</li><li>개인 사업자: <code>0000000000000</code></li></ul> |

<figure><img src="../../.gitbook/assets/contact_mini app.png" alt=""><figcaption></figcaption></figure>{% endstep %}

{% step %}
## [메시징 API 채널 및 LINE 공식 계정 생성 (OA 연동 필수)](https://developers.line.biz/en/docs/messaging-api/getting-started/#create-oa-line-business-id)

&gt; 위치: 제공자 → 새 채널 생성 → 메시징 API → LINE 공식 계정 생성

⚠ MINI 앱은 일본용이므로 인터페이스는 **일본어로만 제공됩니다**.

<figure><img src="../../.gitbook/assets/channel_messaging API.png" alt=""><figcaption></figcaption></figure>다음 항목을 설정하세요:

* SMS 인증 (문자 메시지)
* **アカウント名**: Unifi Apps 이름
* **メールアドレス**: 대표 이메일
* **会社・事業者の所在国・地域**: 국가 선택
* **会社・事業者名**: 법인명
* **業種**: 주요 및 부업종 선택
* **運用目的（複数選択可）**: 해당 목적 선택
* **주요 사용 방법**: 사용 유형 선택
* **비즈니스 매니저 조직 연결 방식**: 적절한 옵션 선택

<figure><img src="../../.gitbook/assets/OA_mini app.png" alt=""><figcaption></figcaption></figure>{% endstep %}

{% step %}
## [LINE 공식 계정에 메시징 API 활성화](https://developers.line.biz/en/docs/messaging-api/getting-started/#using-oa-manager)

&gt; 위치: LINE 공식 계정 → **설정 → 메시징 API 활성화 → 제공자 선택**

<figure><img src="../../.gitbook/assets/OA.png" alt=""><figcaption></figcaption></figure>{% endstep %}

{% step %}
## LINE 공식 계정과 LINE 로그인 채널 연결

&gt; 위치: LINE Developers → 제공자 → LINE 미니앱 채널 → 기본 설정 → 친구 추가 옵션 → 연결된 LINE 공식 계정 → 편집

<figure><img src="../../.gitbook/assets/Link OA.png" alt=""><figcaption></figcaption></figure>{% endstep %}

{% step %}
## 검토 요청

&gt; 위치: LINE Developers → 제공자 → LINE 미니앱 채널 → 검토 요청

* 이전 설정을 모두 완료한 후에만 검토를 요청할 수 있습니다.
* LINE 미니앱 심사는 **LY Corporation**에서 수행합니다.
* Web3 심사를 위해 미니앱 채널에 **Unifi Tech Support Team**을 관리자로 추가해 주세요(기술 지원 채널을 통해 안내 제공).
* 모든 심사가 승인되고 상태가 **반영됨**으로 전환되어야 온보딩이 완료됩니다.

<figure><img src="../../.gitbook/assets/review_mini app.png" alt=""><figcaption></figcaption></figure>{% endstep %}

{% step %}
## **재검증 필수 항목 (중요)**

다음 항목은 승인 후 수정 시 **재검토**가 필요합니다:

* 채널명
* 설명 (현지화)
* 개인정보처리방침 URL
* 엔드포인트 URL
* 연결된 LINE 공식 계정
* 비즈니스 정보 필드
* 연락처 정보 필드

참고:

* 재검토 승인이 완료되기 전까지 변경 사항은 **반영되지 않습니다**.
* 초기 검토 요청 전 정보의 안정성을 반드시 확인하십시오.
{% endstep %}
{% endstepper %}
