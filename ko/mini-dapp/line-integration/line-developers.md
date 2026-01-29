# LINE 개발자

## LINE 플랫폼 통합

LIFF를 통해 Dapp을 구축하려면 9단계가 필요합니다.

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>## [01. LINE 계정으로 LINE Developers 가입](https://developers.line.biz/en/docs/line-developers-console/login-account/#page-title)

LINE 계정 또는 비즈니스 계정으로 LINE Business Developers 계정을 등록하세요. 이 계정은 미니 Dapp에 LINE 서비스를 연동할 때 사용할 수 있습니다.

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>## [02. LINE Developers 개발자 등록용 이메일 추가](https://developers.line.biz/en/docs/line-developers-console/login-account/#register-as-developer)

LINE Developers 계정에 개발자 이름과 이메일을 등록하여 개발자 계정을 생성하세요. LINE Developers에 처음 로그인할 때 이름과 이메일 주소를 등록해야 합니다.

<figure><img src="../../.gitbook/assets/스크린샷 2024-12-12 오후 8.37.07.png" alt=""><figcaption></figcaption></figure>## [03. 제공자 생성](https://developers.line.biz/en/docs/liff/getting-started/#step-one-create-provider)

제공자는 LINE 플랫폼을 통해 서비스를 제공하는 개인, 기업 또는 단체일 수 있습니다.

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>## [04. 채널 생성](https://developers.line.biz/en/docs/liff/getting-started/#step-one-create-provider)

채널은 LINE 플랫폼 기능과 제공자의 서비스 간 소통 경로입니다. 채널은 이름, 설명, 아이콘 이미지를 반드시 설정해야 합니다. \
<mark style="color:red;">**LINE 미니 앱을 구축하려면 채널 생성 시 반드시 &#x27;LINE 로그인&#x27; 유형을 선택해야 합니다.**</mark>

\
블록체인 서비스 및 LINE 미니 앱 유형은 Dapp 포털과 무관합니다.

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>## [05. LINE 공식 계정 생성](https://developers.line.biz/en/docs/messaging-api/getting-started/#create-oa-line-business-id)

4단계에서 생성한 채널에 통합할 메시징 API를 사용하려면 LINE 공식 계정을 생성해야 합니다.

<mark style="color:red;">**미니 앱 발행자의 실제 국가/지역을 &quot;회사 또는 소유자의 국가/지역&quot;으로 선택하십시오</mark>

.

<mark style="color:red;">**</mark>

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>## [06. 공식 계정에서 메시징 API 활성화](https://developers.line.biz/en/docs/messaging-api/getting-started/#create-oa-line-business-id)

5단계에서 LINE 공식 계정 생성 완료 시, LINE 공식 계정 관리자 – 설정 페이지에서 메시징 API 기능을 활성화해야 합니다. LINE 공식 계정 관리자에서 메시징 API 사용을 활성화하면 동일한 제공자(Provider) 하위에서 LINE 개발자 콘솔에 메시징 API 채널이 자동 생성됩니다.

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>## 07. 공식 계정을 LINE 개발자 채널에 연동하기

메시징 API를 활성화한 후 기본 설정 페이지에서 공식 계정을 채널에 연결할 수 있습니다.

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>## [08. LIFF 환경 설정](https://developers.line.biz/en/docs/messaging-api/getting-started/#create-oa-line-business-id)

LIFF SDK를 사용하려면 채널에 미니 앱 URL을 추가하고 LIFF ID를 획득해야 합니다. LINE 개발자 콘솔의 채널 &gt; LIFF 탭에서 LIFF 애플리케이션을 설정할 수 있습니다.

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>## [09. LIFF SDK를 통한 앱 구축](https://developers.line.biz/en/docs/messaging-api/getting-started/#create-oa-line-business-id)

8단계를 완료했다면 LIFF SDK를 사용하여 미니 앱을 LIFF 버전으로 구축할 수 있습니다.
