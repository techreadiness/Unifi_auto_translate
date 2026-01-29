# 공식 계정

## 개요

LINE 공식 계정(OA)은 공지사항, 온보딩, 마케팅 캠페인, 고객 지원 등 유니파이 앱의 커뮤니케이션 채널로 활용됩니다.

OA 생성 방법에 대한 자세한 안내는 다음을 참조하세요:

[계정 생성 | LINE for Business &gt;](https://www.linebiz.com/jp-en/other/)

## **LINE 공식 계정 유형**

### **미인증 OA (권장)**

* LINE 현지 법인의 승인 불필요
* 즉시 사용 가능하며 Unifi Apps와 간편한 연동
* 모든 Unifi Apps 온보딩 사례에 권장

### **인증된 OA**

* **일본, 태국 또는 대만** 현지 LINE 법인 승인 필요
* 승인 절차에 오랜 시간 소요될 수 있음(보통 3개월 이상)
* 법적으로 요구되지 않는 한 권장하지 않음

## OA 프로필 (필수)

프로필(이름, 아이콘, 설명)은 Unifi Apps와 동일한 스타일 및 브랜딩을 따라야 합니다.

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>## OA 콘텐츠

<figure><img src="../../.gitbook/assets/스크린샷 2025-02-04 오전 9.33.07.png" alt=""><figcaption></figcaption></figure>### 환영 메시지

#### 텍스트

* **기본 언어:** 영어\
  (OA는 전 세계적으로 접근 가능하므로 기본 언어로 영어가 필수입니다.)
* **선택 언어:** 일본어, 태국어, 중국어
* 단일 환영 메시지에 여러 언어를 포함하는 것이 허용됩니다.

#### 리치 메시지

* 리치 메시지에는 설명 텍스트와 함께 **이미지 또는 동영상**을 포함할 수 있습니다.
* **CTA URL**이 필수입니다(예: 유니피 앱 URL).

### 리치 메뉴 설정

&gt; 위치: LINE 공식 계정 &gt; 홈 &gt; 채팅 화면 &gt; 리치 메뉴 &gt; 메뉴 내용 설정

#### **언어**

* 기본값: **영어**

#### **템플릿 가이드라인**

다음 구조는 Unifi Apps로의 사용자 전환율 향상에 최적화되어 있습니다:

<figure><img src="../../.gitbook/assets/richmenu-template-guide-03.png" alt="" width="375"><figcaption></figcaption></figure>

<table><thead><tr><th width="205.40631103515625">섹션</th><th>설명</th></tr></thead><tbody><tr><td>A</td><td>유니파이 앱용 LINE 미니 앱 URL 또는 LINE 로그인 LIFF URL</td></tr><tr><td>B &amp; C</td><td><ul><li><strong>섹션 A에 LINE MINI 앱 URL이 포함된 경우, 섹션 B에 LINE 로그인 LIFF URL을 삽입하세요.</strong></li><li><strong>그 외의 모든 섹션에는 소셜 미디어, 웹사이트 또는 관련 채널의 URL을 삽입하십시오.</strong></li></ul></td></tr><tr><td>C</td><td><ul><li><p>Unifi URL</p><ul><li>이미지: 유니피 아이콘 + 유니피 워드마크 (제공됨)</li><li>URL: 미정</li></ul></li></ul></td></tr></tbody></table>{% file src=&quot;../../.gitbook/assets/Unifi_Symbol_400x400 (1).png&quot; %}

## 메시지 전송

* 특정 사용자에게 메시지를 보내거나, 봇을 운영하거나, OA를 외부 시스템과 연동하려면 **메시징 API**를 사용해야 합니다.
* [메시징 API &gt;](https://developers.line.biz/en/docs/messaging-api/)

## **(선택 사항) 다국어 환영 메시지 자동화**

<table><thead><tr><th>단계</th><th width="697">상세 내용</th></tr></thead><tbody><tr><td>1</td><td>LINE Developers에서 OA 채널 생성.</td></tr><tr><td>2</td><td><ul><li>OA 채널의 웹훅 이벤트를 수신하기 위한 API를 구현합니다(8단계에서 사용됨).</li><li>메소드 : POST</li><li><strong>URL</strong>: 자유</li><li><a href="https://developers.line.biz/en/docs/messaging-api/receiving-messages/#webhook-event-in-one-on-one-talk-or-group-chat">웹훅 </a>사양을 참조하십시오.</li><li><a href="https://developers.line.biz/en/docs/messaging-api/receiving-messages/#verify-signature">웹훅 서명을 확인하는 것이 좋습니다.</a></li></ul></td></tr><tr><td>3</td><td>웹훅을 통해 <a href="https://developers.line.biz/en/reference/messaging-api/#follow-event">팔로우 이벤트를 </a>수신하면 요청 본문의 <code>userId</code> 요청 본문의</td></tr><tr><td>4</td><td><ul><li>검색된 <code>userId</code> 를 사용하여 LINE에서 사용자의 언어 설정을 가져옵니다.</li><li>LINE Developers의 Messaging API 탭에서 발급된 채널 액세스 토큰을 사용하십시오.</li><li><a href="https://developers.line.biz/en/reference/messaging-api/#get-profile">Get Profile API</a>를 활용하여 사용자의 언어를 검색합니다.</li></ul></td></tr><tr><td>5</td><td><ul><li>OA 메시징용 템플릿을 생성하세요. 각 로케일에 필요한 콘텐츠를 여러 언어로 구성하고 템플릿을 로컬 또는 클라우드에 저장하세요. 템플릿 서식 지정은 <a href="https://developers.line.biz/en/reference/messaging-api/#message-objects">Message Objects API</a>를 참조하세요.</li><li><p>예시: 한국어와 영어 지원을 위해 템플릿을 다음과 같이 저장합니다:</p><ul><li>oa_ko.json </li><li>oa_en.json</li></ul></li></ul></td></tr><tr><td>6</td><td>4단계에서 가져온 사용자의 언어에 따라 적절한 템플릿을 로드하고 <a href="https://developers.line.biz/en/reference/messaging-api/#send-push-message">OA Send API</a>를 호출합니다.</td></tr><tr><td>7</td><td>LINE Developers에서 <strong>메시징 API</strong> 탭에 접속합니다.<br><img src="../../.gitbook/assets/image-2025-1-9_15-47-22.png" alt=""></td></tr><tr><td>8</td><td><ul><li>1~6단계에서 개발한 API 엔드포인트를 웹훅 URL로 설정합니다.</li><li><strong>웹훅 사용</strong> 옵션을 ON으로 설정합니다.</li></ul><p><img src="../../.gitbook/assets/image-2025-1-9_15-48-4.png" alt="" data-size="original"></p></td></tr><tr><td>9</td><td><p>8단계를 완료하면 팔로워에게 해당 언어로 자동화된 환영 메시지가 전송됩니다.</p><p>(*기존 공식 계정 관리자에서 환영 메시지 설정을 반드시 OFF로 전환하세요.)</p></td></tr></tbody></table>## LINE 오픈챗 (선택 사항)

* 공식 계정 외부 양방향 소통에 유용함
* **일본, 태국, 대만**에서만 이용 가능
* 해당 국가에서 오픈챗 생성 시 해당 국가에 등록된 LINE 계정 필수
* **번역 봇 1개** 추가 가능
  * 예시: 한국어 ↔ 영어 자동 번역

<figure><img src="../../.gitbook/assets/스크린샷 2024-12-12 오후 12.19.26.png" alt="" width="563"><figcaption></figcaption></figure>
