---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/mini-dapp/line-integration/line-developers
---

# LINE Developers

## Integrate LINE Platform

There are 9 steps that need to be taken to build a Dapp via LIFF.

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

## [01. On board to LINE Developers via LINE Account](https://developers.line.biz/en/docs/line-developers-console/login-account/#page-title)

Sign up LINE Business Developers account using your LINE Account or business account. You can use this account when you integrate LINE services to your Mini Dapp.

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

## [02. Add an Email for LINE Developers to be registered as Developer.](https://developers.line.biz/en/docs/line-developers-console/login-account/#register-as-developer)

Register Developer name and email to LINE Developers account to create a developer account. When you first log in to the LINE Developers, You need to register name and email address.

<figure><img src="../../.gitbook/assets/스크린샷 2024-12-12 오후 8.37.07.png" alt=""><figcaption></figcaption></figure>

## [03. Create Provider](https://developers.line.biz/en/docs/liff/getting-started/#step-one-create-provider)

A Provider can be an individual, company or organization that provides services through the LINE Platform.

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

## [04. Create Channel](https://developers.line.biz/en/docs/liff/getting-started/#step-one-create-provider)

A Channel is a communication path between the LINE Platform’s functions and a provider’s services. Channels must have a name, description and icon image. \
<mark style="color:red;">**You MUST select LINE Login type when you create Channel to build LINE Mini Dapp.**</mark> \
Blockchain Service and LINE MINI App type are not related to Dapp Portal.

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

## [05. Create LINE Official Account](https://developers.line.biz/en/docs/messaging-api/getting-started/#create-oa-line-business-id)

You should create LINE Official Account to use Messaging API which is to be integrated to Channel you’ve created from Step 4.

<mark style="color:red;">**Please select "Company or owner's country or region" as the actual country of origin for Mini Dapp publisher.**</mark>

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

## [06. Enable Messaging API from Official Account](https://developers.line.biz/en/docs/messaging-api/getting-started/#create-oa-line-business-id)

If you have created successfully LINE Official Account from Step5, you should enable Messaging API function on LINE Official Account Manager – Setting page. When enabling the use of Messaging API in the LINE Official Account Manager, a Messaging API channel is created on LINE Developer’s console under same Provider automatically.

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

## 07. Integrate Official Account to LINE Developer’s Channel

Once Messaging API is enabled, you can link Official Account to Channel on Basic setting page.

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

## [08. Set LIFF Environment](https://developers.line.biz/en/docs/messaging-api/getting-started/#create-oa-line-business-id)

To use LIFF SDK, You need to add the Mini Dapp URL to your channel and get LIFF ID. You can set LIFF applications on LINE Developers Console – Channel – LIFF tab.

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

## [09. Build App via LIFF SDK](https://developers.line.biz/en/docs/messaging-api/getting-started/#create-oa-line-business-id)

If you’ve completed Step 8, You can build Mini Dapp as LIFF version using LIFF SDK.
