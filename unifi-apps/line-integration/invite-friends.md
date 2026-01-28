# Invite Friends

## Overview

The Invite Friends feature is available in LINE Versions (LINE MINI App and LINE Login LIFF).\
This feature is one of the most important tools for **user acquisition** and **user activation**, helping your Unifi Apps grow organically within the LINE ecosystem.

Referrals play a key role in driving viral spread among LINE users.\
We strongly recommend implementing this feature to maximize visibility and user engagement.

## Invite Friends Support by Version

| Version         | Invite Friends | Notes                           |
| --------------- | -------------- | ------------------------------- |
| LINE MINI App   | Yes            | ShareTargetPicker supported     |
| LINE Login LIFF | Yes            | ShareTargetPicker supported     |
| Web             | No             | implement via referral URL copy |

## How to Implement (Using LIFF APIs)

To use the Invite Friends feature, refer to the following LIFF APIs:

* [Sending Messages](https://developers.line.biz/en/docs/liff/developing-liff-apps/#sending-messages)
* [ShareTargetPicket](https://developers.line.biz/en/docs/liff/developing-liff-apps/#share-target-picker)

### Restricting Message Targets

If you want to ensure that messages are sent **only to the user’s LINE friends**, and not to other Official Accounts or group chats, set:\
[options.isMultiple as false >](https://developers.line.biz/en/reference/liff/#share-target-picker-arguments)

```
options.isMultiple = false;
```

## **Example UI**

Below is an example of the “Invite a Friend” screen.

<figure><img src="../../.gitbook/assets/스크린샷 2024-12-12 오후 3.55.06.png" alt=""><figcaption></figcaption></figure>
