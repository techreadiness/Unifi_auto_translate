---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/unifi-apps/line-integration/line-login-liff
---

# LINE 로그인 LIFF

{% stepper %}
{% step %}
## [LINE 비즈니스 ID 생성 및 LINE Developers 로그인](https://developers.line.biz/en/)

* 개인 LINE 계정 또는 이메일로 로그인
* LINE Developers 콘솔에 접근하기 위한 비즈니스 ID 생성

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
## [LINE 로그인 채널 생성](https://developers.line.biz/en/docs/liff/getting-started/#step-one-create-provider)

<figure><img src="../../.gitbook/assets/channel_LIFF.png" alt="" width="563"><figcaption></figcaption></figure>| 필드                                | 값                               |
| ------------------------------------ | ----------------------------------- |
| 서비스 제공 지역                 | 대상 서비스 국가 선택       |
| 회사 또는 소유자 국가/지역         | 법인 소재 국가 선택     |
| 채널 이름                         | Unifi 앱 이름 입력               |
| 채널 설명                          | 간단한 서비스 설명 입력 |
| 앱 유형                            | **웹 앱** 선택                  |

<figure><img src="../../.gitbook/assets/developers.line.biz_console_channel_new_provider=2004696501&#x26;type=line-login.png" alt="" width="563"><figcaption></figcaption></figure>{% endstep %}

{% step %}
## [LIFF 생성](https://developers.line.biz/en/docs/liff/registering-liff-apps/#registering-liff-app)

&gt; 위치: LINE Developers → 제공자 → LINE 로그인 채널 → **LIFF** 탭 → 추가

| 필드             | 값                                     |
| ----------------- | ----------------------------------------- |
| LIFF 앱 이름     | 유니파이 앱 이름 입력                     |
| 크기              | 전체                                      |
| 엔드포인트 URL      | 유니파이 앱 URL 입력                      |
| 스코프            | `openid` (필수), `profile` (선택) |
| 친구 추가 옵션 | 켜기 (일반)                               |

<figure><img src="../../.gitbook/assets/developers.line.biz_console_channel_new_provider=2004696501&#x26;type=line-login (1).png" alt="" width="563"><figcaption></figcaption></figure>{% endstep %}

{% step %}
## [메시징 API 채널 및 LINE 공식 계정 생성 (OA 연동 필수)](https://developers.line.biz/en/docs/messaging-api/getting-started/#create-oa-line-business-id)

&gt; 위치: LINE Developers → 제공자 → 새 채널 생성 → **메시징 API**

<figure><img src="../../.gitbook/assets/channel_messaging API.png" alt=""><figcaption></figcaption></figure>다음 항목 설정:

* SMS 인증: 문자 메시지
* 계정명: Unifi Apps 이름
* 이메일 주소: 대표 이메일
* 법인 소재 국가/지역
* 회사명: 법인명
* 업종: 주요 및 하위 카테고리 선택

<figure><img src="../../.gitbook/assets/Create OA.png" alt="" width="524"><figcaption></figcaption></figure>{% endstep %}

{% step %}
## [LINE 공식 계정에 메시징 API 활성화](https://developers.line.biz/en/docs/messaging-api/getting-started/#using-oa-manager)

&gt; 위치: LINE 공식 계정 → **설정 → 메시징 API 활성화 → 제공자 선택**

<figure><img src="../../.gitbook/assets/OA.png" alt=""><figcaption></figcaption></figure>{% endstep %}

{% step %}
## LINE 공식 계정과 LINE 로그인 채널 연결

&gt; 위치: LINE Developers → 제공자 → LINE 로그인 채널 → **기본 설정** →\
&gt; 친구 추가 옵션 → 연결된 LINE 공식 계정 → 편집 → 생성된 OA 선택

<figure><img src="../../.gitbook/assets/Link OA.png" alt=""><figcaption></figcaption></figure>{% endstep %}

{% step %}
## LINE 로그인 LIFF(프로덕션) 게시하기

&gt; 위치: LINE Developers → 제공자 → LINE 로그인 채널 → **개발 중 → 게시**

데모 제출을 위해서는 LIFF를 프로덕션 환경에 게시해야 합니다.

_개발 중_ 상태에서는 LIFF 접근이 제한되어 데모 심사가 진행되지 않습니다.

<figure><img src="../../.gitbook/assets/publish.png" alt=""><figcaption></figcaption></figure>{% endstep %}
{% endstepper %}
