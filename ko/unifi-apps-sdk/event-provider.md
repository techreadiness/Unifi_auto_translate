# 이벤트 제공자

<figure><img src="../.gitbook/assets/EventProvider_Unifi Apps Server.png" alt=""><figcaption></figcaption></figure>## 이벤트 제공자 콜백

### DappPortalSDK.getEventProvider()

Unifi 앱 미션 완료 시 이벤트 제공자 콜백

* 이 콜백 메서드의 목적은 Unifi 측에서 미션 완료를 검증하고, 검증이 성공할 경우 자동으로 성공 배너를 표시하는 것입니다.

```javascript
const eventProvider = DappPortalSDK.getEventProvider();

// 미션 완료 시
const eventId: string = &quot;eventId&quot;;          // Unifi에서 제공한 고유 이벤트 ID
const subMissionIndex: string = &quot;1&quot;;        // 하위 미션 인덱스 (0부터 시작)

await eventProvider.callback(eventId, subMissionIndex); // 검증 성공 시 자동으로 배너 표시
```

**매개변수**

<table><thead><tr><th width="164.28125">매개변수</th><th width="82.5703125">유형</th><th>설명</th></tr></thead><tbody><tr><td>eventId</td><td>string</td><td><strong>Unifi</strong>에서 제공하는 고유 식별자</td></tr><tr><td>subMissionIndex</td><td>문자열</td><td>Unifi에서 제공하는 하위 미션의 인덱스입니다. 인덱싱은 0부터 시작합니다.<br>예시<br>:- 이벤트 아이템 구매 미션 -&gt; subMissionIndex = &quot;0&quot;<br>사용- Lv4 달성 미션 -&gt; subMissionIndex = &quot;1&quot; 사용</td></tr></tbody></table>

**응답**

해당 없음

* 검증이 성공하면 배너가 표시됩니다.

## Unifi Apps 서버 REST API 구현

#### **Unifi Apps 서버 REST API 구현 가이드** 

Unifi 차트에서 **미션 완료** 기능을 활성화하려면, Unifi Apps 서버가 미션 완료 여부를 검증할 수 있는 API 엔드포인트를 제공해야 합니다.

* **필요 정보**
  * API URL (필수)
  * 커스텀 헤더 (선택 사항)
* **API 개요**
  * 메서드**:** <mark style="color:blue;">`GET`</mark>
  * 스킴**:** `https`
  * 읽기 시간 제한**:** `1초`
    * Unifi 서버가 **1초** 이내에 응답을 받지 못하면 미션은 **실패**로 처리됩니다.
* **사용자 정의 헤더 (선택 사항)**
  * API 호출 시 사용자 정의 헤더를 포함할 수 있습니다.
  * 헤더 키/값 형식에 **제한 사항**은 없습니다.
  * **하나만** 사용할 수 있으며, **선택 사항**입니다.
  * 예) x-dapp-custom-key: gq8g0Ah1MD98
* **URL 형식**
  * 기본 URL**:** Unifi Apps 서버 URL
  * 쿼리 매개변수로 `$identifier`를 반드시 포함해야 합니다.
  * `$identifier`는 Unifi 서버에서 사용자의 지갑 주소(소문자)로 대체될 자리 표시자입니다.
  * 예) https://example.dapp.io/api/mission/1111?param=zzzz&amp;**identifier=$identifier**
* **응답 본문**
  * 콘텐츠 유형**:** JSON
  * Unifi 서버가 성공적인 응답을 수신하면 사용자가 미션을 완료한 것으로 간주됩니다.
    * 미션 완료
    * ```json
      HTTP/1.1 200 OK
      {
        &quot;result&quot;: true
      }
      ```
    * 미션 실패
    * ```json
      HTTP/1.1 200 OK
      {
        &quot;result&quot;: false
      }
      ```
