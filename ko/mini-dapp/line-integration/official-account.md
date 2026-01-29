# 공식 계정

## 가이드

자세한 내용은 [계정 생성 | LINE for Business](https://www.linebiz.com/jp-en/other/)를 참조하세요.

### 미인증 OA 생성 및 미니 앱 연동

* 미인증 OA: 별도의 LINE 현지 법인 승인이 필요 없는 공식 계정입니다.
* 인증된 OA: 일본, 태국, 대만 현지 LINE 법인으로부터 승인을 받은 OA입니다.
  * 인증된 공식 계정을 생성하려면 현지 법인의 승인이 필요하며, 승인 절차에 시간이 소요될 수 있음을 유의하시기 바랍니다.

### OA 프로필 (필수)

미니 앱과 동일한 컨셉을 사용하십시오.

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>### OA 콘텐츠

<figure><img src="../../.gitbook/assets/스크린샷 2025-02-04 오전 9.33.07.png" alt=""><figcaption></figcaption></figure>#### 환영 메시지 (텍스트)

언어

* 기본: 영어 (OA 채널은 전 세계 사용자가 접근 가능한 공개 채널이므로 기본적으로 영어로 메시지를 설정해 주시기 바랍니다.)
* 선택: 일본어, 태국어, 중국어
* 다양한 언어로 작성된 환영 메시지를 하나의 채팅으로 전송할 수 있습니다.

#### 환영 메시지 (리치)

일반 텍스트 메시지와 함께 이미지 또는 동영상을 사용할 수 있습니다. (CTA URL 필수)

#### 리치 메뉴

기본 언어는 영어입니다.

#### 템플릿

* 아래 템플릿 가이드에 따라 리치 메뉴 이미지를 제작하고 URL을 설정해 주세요.
  이 템플릿은 사용자가 Dapp으로 전환하도록 유도하는 최적의 흐름입니다. 리치 메뉴 이미지 제작 시 깔끔하고 전환율 중심의 디자인이 필요합니다.

<figure><img src="../../.gitbook/assets/richmenu-template-guide-03.png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image-2025-1-9_14-19-35.png" alt=""><figcaption></figcaption></figure>* **A**
  * URL: 미니 Dapp URL (LIFF)
* **B &amp; C**
  * URL: 미니 Dapp 소셜 채널, 웹사이트 URL 등
* **D**
  * (필수) 공식 LINE 미니 Dapp으로서, 이 섹션은 Dapp 포털로의 경로를 제공하고 Dapp 간 크로스셀링을 유도합니다.
  * **이미지**: 미니 앱 아이콘 + 포털 워드마크 (첨부)
  * URL: [https://liff.line.me/2006533014-8gD06D64](https://liff.line.me/2006533014-8gD06D64) (앱 포털 LIFF)
* 이미지 파일

{% file src=&quot;../../.gitbook/assets/Portal.png&quot; %}

{% file src=&quot;../../.gitbook/assets/Portal_white.png&quot; %}

{% file src=&quot;../../.gitbook/assets/(Dapp) Portal.png&quot; %}

### 메시지

* 특정 사용자에게 메시지를 전송하거나, BOT을 사용하거나, OA를 외부 서비스와 연동하려면 [메시지 API](https://developers.line.biz/en/docs/messaging-api/)를 사용해야 합니다. 이 경우 첨부된 메시지 API URL을 참고하시기 바랍니다.

### 권장사항) 다국어 환영 메시지 운영 (추가 개발 필요)

* 추가 개발을 통해 사용자가 OA 채널을 팔로우할 때 언어 설정에 맞춰 환영 메시지를 발송할 수 있습니다. (자세한 내용은 아래 가이드 참조)



<table><thead><tr><th>단계</th><th width="697">상세 내용</th></tr></thead><tbody><tr><td>1</td><td>LINE Developers에서 OA 채널 생성</td></tr><tr><td>2</td><td><ul><li>OA 채널의 웹훅 이벤트를 수신하기 위한 API를 구현합니다(8단계에서 사용됨).</li><li>메소드 : POST</li><li><strong>URL</strong>: 자유</li><li><a href="https://developers.line.biz/en/docs/messaging-api/receiving-messages/#webhook-event-in-one-on-one-talk-or-group-chat">웹훅 </a>사양을 참조하십시오.</li><li><a href="https://developers.line.biz/en/docs/messaging-api/receiving-messages/#verify-signature">웹훅 서명을 확인하는 것이 좋습니다.</a></li></ul></td></tr><tr><td>3</td><td>웹훅을 통해 <a href="https://developers.line.biz/en/reference/messaging-api/#follow-event">팔로우 이벤트를 </a>수신하면 요청 본문의 <code>userId</code> 요청 본문의</td></tr><tr><td>4</td><td><ul><li>검색된 <code>userId</code> 를 사용하여 LINE에서 사용자의 언어 설정을 가져옵니다.</li><li>LINE Developers의 Messaging API 탭에서 발급된 채널 액세스 토큰을 사용하십시오.</li><li><a href="https://developers.line.biz/en/reference/messaging-api/#get-profile">Get Profile API</a>를 활용하여 사용자의 언어를 검색합니다.</li></ul></td></tr><tr><td>5</td><td><ul><li>OA 메시징용 템플릿을 생성하세요. 각 로케일에 필요한 콘텐츠를 여러 언어로 구성하고 템플릿을 로컬 또는 클라우드에 저장하세요. 템플릿 서식 지정은 <a href="https://developers.line.biz/en/reference/messaging-api/#message-objects">Message Objects API</a>를 참조하세요.</li><li><p>예시: 한국어와 영어 지원을 위해 템플릿을 다음과 같이 저장합니다:</p><ul><li>oa_ko.json </li><li>oa_en.json</li></ul></li></ul></td></tr><tr><td>6</td><td>4단계에서 가져온 사용자의 언어에 따라 적절한 템플릿을 로드하고 <a href="https://developers.line.biz/en/reference/messaging-api/#send-push-message">OA Send API</a>를 호출합니다.</td></tr><tr><td>7</td><td>LINE Developers에서 <strong>메시징 API</strong> 탭에 접속합니다.<br><img src="../../.gitbook/assets/image-2025-1-9_15-47-22.png" alt=""></td></tr><tr><td>8</td><td><ul><li>1~6단계에서 개발한 API 엔드포인트를 웹훅 URL로 설정합니다.</li><li><strong>웹훅 사용</strong> 옵션을 ON으로 설정합니다.</li></ul><p><img src="../../.gitbook/assets/image-2025-1-9_15-48-4.png" alt="" data-size="original"></p></td></tr><tr><td>9</td><td><p>이제부터 사용자가 OA를 팔로우할 때마다 해당 사용자의 언어로 웰컴 메시지가 자동으로 발송됩니다.</p><p>(*기존 공식 계정 관리자에서 환영 메시지 설정을 반드시 OFF로 전환해 주세요.)</p></td></tr></tbody></table>### OA 동의는 미니앱(LIFF) 채널 동의 직후 설정해야 합니다

* 사용자가 미니앱(LIFF)에 처음 연결할 때, 사용자는 미니앱(LIFF)의 채널에 동의해야 합니다. 채널 동의는 별도로 생성되지 않으며, 미니앱이 LIFF로 생성될 때 기본적으로 생성되며 동의 절차가 사용자에게 표시됩니다.
  * 채널 동의 직후 &#x27;OA 친구 추가&#x27; 팝업을 연결할 수 있습니다. 따라서 채널 동의 후 OA 동의를 설정하는 방법은 아래 문서를 참고하세요. \
    <mark style="color:red;">**공격적 모드(AGGRESIVE VERSION)를 선택해야 합니다.**</mark>

* OA 공격적 모드 설정 방법
    * LINE Developers &gt; LINE 로그인 채널 &gt; LIFF &gt; 친구 추가 옵션으로 이동하여 &#x27;On(공격적)&#x27;으로 설정합니다.

<figure><img src="../../.gitbook/assets/스크린샷 2024-12-12 오후 12.12.20.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/스크린샷 2025-04-16 오후 1.12.08.png" alt=""><figcaption></figcaption></figure>## 공식 계정 구독 요금제

<figure><img src="../../.gitbook/assets/스크린샷 2024-12-12 오후 12.18.22.png" alt=""><figcaption></figcaption></figure>#### 이는 하나의 OA 운영 비용이며, 여러 OA의 비용은 누적됩니다.



## LINE 오픈챗

#### 오픈챗은 OA 외부에서 양방향 커뮤니케이션에 활용할 수 있습니다.

* 오픈챗은 일본, 태국, 대만 지역 사용자만 이용 가능합니다.
* 일본, 태국, 대만에서 오픈챗을 생성하려면 해당 국가별 LINE 계정이 필요합니다. 예를 들어, 일본 오픈챗 생성 시 일본 계정이 필요합니다.
* 오픈챗에 번역 봇을 추가할 수 있습니다. 단일 언어만 추가 가능하며 대상 국가에 맞는 번역 봇 사용을 권장합니다.
  * 예시) 한국어&lt;&gt;영어 봇 추가 시, 사용자가 한국어로 채팅하면 자동으로 영어로 번역됩니다. 영어로 작성 시 자동으로 한국어로 번역됩니다.

<figure><img src="../../.gitbook/assets/스크린샷 2024-12-12 오후 12.19.26.png" alt="" width="563"><figcaption></figcaption></figure>
