# DappPortalSDK 초기화

## SDK 초기화

#### 1. `init()` 메서드를 통한 SDK 초기화

```javascript
import DappPortalSDK from &#x27;@linenext/dapp-portal-sdk&#x27;

const sdk = await DappPortalSDK.init({ clientId: &#x27;<client_id>&#x27;, chainId: &#x27;1001&#x27; });
```

**매개변수**

| 이름                                                               | 설명                                                                                                                                           |
| ------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |<p>클라이언트 <mark style="color:red;">ID*필수</mark><br>문자열</p>
|  | SDK 신청 시 제공된 clientId                                                                                                       |
|<p>체인 ID<br>문자열</p>                                            |<p>기본값은 <strong>1001</strong>(테스트넷)입니다. 개발 후<br>메인넷을 사용하려면 값을 <strong>8217</strong>(메인넷)으로 설정하세요.</p>  |

**응답**\
`DappPortalSDK` 객체를 반환하며, 이를 통해 다음 메서드를 호출할 수 있습니다.

```
DappPortalSDK
```

| 메서드 이름                                                       | 설명                                                                     |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| **getWalletProvider**  <mark style="color:blue;">함수</mark>  | 지갑 제공자 초기화                                                       |
| **getPaymentProvider** <mark style="color:blue;">함수</mark>  | 결제 제공자 초기화                                                      |
| **isSupportedBrowser** <mark style="color:blue;">함수</mark>  | 현재 브라우저가 지원되는 경우 `true`를 반환하고, 그렇지 않으면 `false`를 반환합니다. |

<mark style="color:green;">**DappPortalSDK.init()은 단 한 번만 실행하고 싱글톤 객체로 관리할 것을 강력히 권장합니다. 지갑에 요청할 때마다 DappPortalSDK.init()을 호출하여 새 DappPortalSDK 객체를 생성하면 오작동을 유발할 수 있습니다. 싱글톤으로 강제하지 않는 이유는 다중 구성이 필요한 시나리오를 지원하기 위함입니다. 예를 들어, 단일 앱에서 테스트넷과 메인넷을 모두 사용하려는 경우입니다. 이러한 경우에도 테스트넷용 싱글톤 DappPortalSDK 객체 하나와 메인넷용 싱글톤 객체 하나를 관리할 것을 권장합니다.**</mark></client_id>
