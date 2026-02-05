---
hidden: true
metaLinks:
  alternates:
    - https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/join-us-1
---

# Join Us

## ✅ Unifi Apps 온보딩 가이드

Unifi Apps는 다양한 버전 조합을 통해 온보딩할 수 있습니다. 개발자는 자신의 서비스 아키텍처와 타겟 사용자에게 가장 적합한 옵션을 선택할 수 있습니다.

**지원 가능한 버전 조합**

* LINE MINI App & LINE Login LIFF & Web
* LINE MINI App & Web
* LINE Login LIFF & Web
* LINE MINI App or Web (Single Type)

📌 주의

* LINE Login LIFF는 기술적으로 Web 서비스 위에서 구현되므로, Single Type(단독 형태)으로 선택할 수 없습니다. 따라서 LINE Login LIFF를 사용하는 서비스는 반드시 Web 버전과 함께 런칭해야 합니다.



**Supported Onboarding Types**

| Version         | Operating Env & Supported Features                                                 | Target Users   | Target Regions | Onboarding Requirements                                                                                                                 | SDK Feature Differences                           | Demo Submission Authority |
| --------------- | ---------------------------------------------------------------------------------- | -------------- | -------------- | --------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- | ------------------------- |
| LINE MINI App   | Runs within the LINE mobile app environment and supports Unifi featured placements | LINE users     | Japan          | Applicable only to entities possessing a Japanese Corporate Number (Hōjin Bangō) or individual business owners with Japanese residency. | Supports **IAP payments only**                    | LY & LINE NEXT            |
| LINE Login LIFF | Runs within the LINE mobile app environment and supports Unifi featured placements | LINE users     | Global         | -                                                                                                                                       | Supports **Crypto & STRIPE (Fiat) payments only** | LINE NEXT                 |
| Web             | Runs within general web browsers and supports Unifi featured placements            | Non-LINE users | Global         | -                                                                                                                                       | Supports **Crypto & STRIPE (Fiat) payments only** | LINE NEXT                 |

## 1. Submit Unifi Apps Application

To begin onboarding, please submit the designated **Unifi Apps application form**.\
The information provided will be used to evaluate service eligibility and onboarding readiness.

[Apply for Unifi Apps >](https://tally.so/r/D4BNjp)

## 2. Internal Review

Our team will review the submitted application to determine eligibility for Unifi Apps onboarding.

* The internal review will primarily focus on LINE Mini App launch eligibility, core game mechanics, and materials submitted in the application form.
* A dedicated BD (Business Development) manager may be assigned at this stage to support early coordination

## 3. Onboarding Process Initiation

* Once your service passes the internal review, we will provide the Unifi Apps SDK Terms & Conditions form along with other required onboarding materials, including the due diligence form and the Dapp Information Registration form.
* Please review and submit the Unifi Apps SDK Terms & Conditions as instructed.&#x20;
* Upon acceptance, the Unifi Apps SDK—along with all required authentication credentials—will be provisioned.&#x20;
* The SDK will be delivered to your registered email address within approximately three (3) business days.

## 4. Develop Unifi Apps Demo

The payment integration method differs depending on the onboarding Version selected.

| Version         | Wallet Integration | Supported Payment Methods       |
| --------------- | ------------------ | ------------------------------- |
| LINE MINI App   | Supported          | IAP payments (_Coming Soon_)    |
| LINE Login LIFF | Supported          | Crypto & Stripe (Fiat) payments |
| Web             | Supported          | Crypto & Stripe (Fiat) payments |

Please develop your Unifi Apps according to the provided Development [checklist](https://docs.dappportal.io/~/revisions/PsJIlYlQPCCZu69maZ4H/unifi-apps-review-guidelines).\
For common issues and troubleshooting tips, you may refer to the [FAQ](https://docs.dappportal.io/~/revisions/PsJIlYlQPCCZu69maZ4H/join-us-1/faq).\
If you have any technical questions during development, please feel free to contact us through the following channels:

* [Telegram Tech Support Channel](../join-us/contact-us.md)
* Email: **dapp-support@linecorp.com**

## 5. Review & Feedback

### Review Authority & Timeline

{% hint style="info" %}
The review process focuses on service eligibility, functional completeness, and compliance requirements.\
**For LINE MINI Apps, an internal review by LINE NEXT is required prior to LY submission.**
{% endhint %}

| Version         | Demo Submission/Review Authority                                                                                                                               | Review Timeline        |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| LINE MINI App   | <ul><li>LINE NEXT (Pre-review)</li><li>LY (Final approval)</li><li>Submission to LY is required <strong>after LINE NEXT review is completed</strong></li></ul> | 5–10 business days     |
| LINE Login LIFF | <ul><li>LINE NEXT</li><li>Submission via email</li></ul>                                                                                                       | Up to  3 business days |
| Web             | <ul><li>LINE NEXT</li><li>Submission via email</li></ul>                                                                                                       | Up to 3 business days  |

📌 _For LINE MINI Apps, LY submission without prior LINE NEXT review is not supported._

### Demo Submission

**LINE MINI App**

* **Review Target**: Staging version
* **Review Process:**
  1. Submit the staging build to **LINE NEXT for pre-review**
     1. **Please add the LINE NEXT review manager as an Admin** in your LINE MINI App channel via the **LINE Developers Console**.
     2. At the time of submission, the **contact details of the assigned reviewer** will be shared with you.
  2. After receiving confirmation from LINE NEXT,\
     request **LY approval through the LINE Developers Console**
* **Review Feedback:**\
  Review feedback will be shared through **LINE NEXT and LY**, depending on the review stage.

📌 _Please note that LINE NEXT pre-review is mandatory before submitting to LY._

**LINE Login LIFF & Web**

* **Review Target**: LINE Login LIFF / Web version
* **Submission Method**: Email submission to **`dapp-support@linecorp.com`**
* The following information must be included in the request email:
  * Name of Unifi Apps&#x20;
  * Demo URL
  * Desired launch date

### After Demo Approval

Once your demo is approved, the onboarding process for the official launch will begin.

* Guidance on launch preparation procedures will be provided
* Operational and technical checks will be conducted

## 6. Launching Unifi Apps

After onboarding is completed, your Unifi Apps will be scheduled for official launch.

* The launch date will be finalized in coordination with your team
* Final technical and operational validations will be completed prior to launch

📌 _Please ensure your team is available to respond promptly to any critical issues during the launch period._

