---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/mini-dapp/line-integration/line-front-end-framework-liff/essential-settings
---

# Essential Settings

## Setting for data collection from LIFF via Mini Dapp SDK

* Go to LINE Developers console
*   Click Channel which integrate LIFF

    <figure><img src="../../../.gitbook/assets/스크린샷 2025-01-14 오후 2.25.06.png" alt=""><figcaption></figcaption></figure>
*   Click LIFF app name<br>

    <figure><img src="../../../.gitbook/assets/스크린샷 2025-01-14 오후 2.25.18.png" alt=""><figcaption></figcaption></figure>
*   Edit Scope checked with 'openid'<br>

    <figure><img src="../../../.gitbook/assets/스크린샷 2025-01-14 오후 2.25.37.png" alt=""><figcaption></figcaption></figure>

## [Enabling the Action Button](https://developers.line.biz/en/docs/liff/overview/#action-button)

To use features such as URL sharing, minimizing the browser, and page refresh within your LIFF Version, you need to enable the action button.

How to set it up: Go to LIFF settings > Options > Module mode > Disable&#x20;

* The action button is only available where Module mode is turn off.

<figure><img src="../../../.gitbook/assets/action button.png" alt="" width="375"><figcaption></figcaption></figure>

## [Set Minimization for LIFF Browser](https://developers.line.biz/en/docs/liff/minimizing-liff-browser/#overview)

When playing a Mini Dapp in a chat room, the user may want to perform another action, such as sending a message to the chat room. In this case, minimizing the LIFF browser will suspend playing the Mini Dapp and allow the user to perform the action without disconnetion from Mini Dapp. After performing the action, the user can resume playing the Mini Dapp by maximizing the LIFF browser.

<figure><img src="../../../.gitbook/assets/스크린샷 2025-01-16 오전 10.45.34.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/스크린샷 2025-01-16 오전 10.46.00.png" alt=""><figcaption></figcaption></figure>



