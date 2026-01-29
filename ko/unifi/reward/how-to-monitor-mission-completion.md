# 미션 완료 모니터링 방법

앱은 유니피 앱스(Unifi Apps) 내에서 구현된 미션 보상(KAIA/USDt, NFT, 포인트)을 등록할 수 있습니다. 각 보상은 다음과 같은 방식으로 유니피 앱스에 등록 및 추적됩니다.

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>Unifi Apps는 앱이 제출한 EOA 지갑(보상용)의 거래 내역을 추적합니다. 해당 지갑에서 특정 사용자의 지갑으로 특정 금액의 거래가 발생하면, Unifi Apps는 미션이 완료되고 보상이 지급된 것으로 인식합니다. 이러한 특성상 여러 미션을 운영할 경우 각 미션별로 별도의 지갑을 준비해야 합니다. 여러 미션의 보상에 동일한 지갑을 사용할 경우, 유니파이 앱은 어떤 미션이 완료되었는지 인식할 수 없습니다.

\*미션 완료 시 보상 지급은 앱에서 구현해야 합니다. KAIA 또는 USDt 송금 관련 정보는 [https://docs.kaia.io/references/json-rpc/references/](https://docs.kaia.io/references/json-rpc/references/)를 참조하십시오.



### NFT 보상

NFT 미션의 추적 구조는 KAIA/USDt 미션과 유사합니다. Unifi Apps는 앱에서 제출된 NFT가 배포되는 EOA 지갑의 거래 내역을 추적하며, 해당 계약 주소(contract address)를 참조합니다. NFT 발행 시 EOA 지갑을 Unifi Apps 팀에 제출해야 하며, Unifi Apps 팀이 해당 지갑으로 NFT를 에어드롭합니다.

\*Unifi Apps의 기능상, 단일 이벤트에서 단일 NFT만 배포될 때 추적이 가능합니다.
