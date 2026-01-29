# 친구 초대

## 개요

친구 초대 기능은 LINE 버전(LINE MINI 앱 및 LINE 로그인 LIFF)에서 이용 가능합니다.
이 기능은 **사용자 확보** 및 **사용자 활성화**를 위한 가장 중요한 도구 중 하나로, LINE 생태계 내에서 유니파이 앱의 유기적 성장을 돕습니다.

추천은 LINE 사용자 간 바이럴 확산을 주도하는 핵심 역할을 합니다.
가시성과 사용자 참여도를 극대화하기 위해 이 기능 구현을 적극 권장합니다.

## 버전별 친구 초대 지원 현황

| 버전         | 친구 초대 | 참고사항                           |
| --------------- | -------------- | ------------------------------- |
| LINE 미니 앱   | 지원됨       | 공유대상선택기 지원     |
| LINE 로그인 LIFF | 지원됨       | 공유대상선택기 지원     |
| 웹             | 지원 안 됨   | 추천 URL 복사 방식으로 구현 |

## 구현 방법 (LIFF API 사용)

친구 초대 기능을 사용하려면 다음 LIFF API를 참조하세요:

* [메시지 전송](https://developers.line.biz/en/docs/liff/developing-liff-apps/#sending-messages)
* [ShareTargetPicket](https://developers.line.biz/en/docs/liff/developing-liff-apps/#share-target-picker)

### 메시지 대상 제한

메시지가 **사용자의 LINE 친구에게만** 전송되고 다른 공식 계정이나 그룹 채팅에는 전송되지 않도록 하려면 다음을 설정하세요:\
[options.isMultiple as false &gt;](https://developers.line.biz/en/reference/liff/#share-target-picker-arguments)

```
options.isMultiple = false;
```

## **예시 UI**

아래는 &quot;친구 초대&quot; 화면의 예시입니다.

<figure><img src="../../.gitbook/assets/스크린샷 2024-12-12 오후 3.55.06.png" alt=""><figcaption></figcaption></figure>
