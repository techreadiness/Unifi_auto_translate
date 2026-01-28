# Official Account

## Overview

A LINE Official Account (OA) is used as a communication channel for Unifi Apps—for announcements, onboarding, marketing campaigns, and customer support.

For detailed instructions on creating an OA, refer to:

[Create an Account | LINE for Business >](https://www.linebiz.com/jp-en/other/)

## **Types of LINE Official Accounts**

### **Unverified OA (Recommended)**

* No approval required from LINE’s local legal entity
* Immediately usable and easy to integrate with Unifi Apps
* Recommended for all Unifi Apps onboarding cases

### **Verified OA**

* Requires approval from LINE local entities in **Japan, Thailand, or Taiwan**
* Approval process could take a long time (often 3+ months)
* Not recommended unless legally required

## OA Profile (Required)

The profile (name, icon, description) should follow the same style and branding as the Unifi Apps.

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

## Contents for OA

<figure><img src="../../.gitbook/assets/스크린샷 2025-02-04 오전 9.33.07.png" alt=""><figcaption></figcaption></figure>

### Welcome Message&#x20;

#### Text

* **Default Language:** English\
  (Since OA is globally accessible, English is required as the default language.)
* **Optional Languages:** Japanese, Thai, Chinese
* It is acceptable to include multiple languages within a single welcome message.

#### Rich Message

* Rich messages may include **images or videos** with descriptive text.
* A **CTA URL** is required (e.g., Unifi Apps URL).

### Rich Menu Setup

> Location: LINE Official Account > Home > Chat screen > Rich menus > Menu content setting

#### **Language**

* Default: **English**

#### **Template Guidelines**

The following structure is optimized to increase user conversion into the Unifi Apps:

<figure><img src="../../.gitbook/assets/richmenu-template-guide-03.png" alt="" width="375"><figcaption></figcaption></figure>

<table><thead><tr><th width="205.40631103515625">Section</th><th>Description</th></tr></thead><tbody><tr><td>A</td><td>LINE MINI App URL or LINE Login LIFF URL for Unifi Apps</td></tr><tr><td>B &#x26; C</td><td><ul><li><strong>If section A contains the LINE MINI App URL, insert the LINE Login LIFF URL in section B.</strong></li><li><strong>For all other sections, insert URLs for social media, the website, or related channels.</strong></li></ul></td></tr><tr><td>C</td><td><ul><li><p>Unifi URL</p><ul><li>Image: Unifi Icon + Unifi Wordmark (provided)</li><li>URL: TBD</li></ul></li></ul></td></tr></tbody></table>

{% file src="../../.gitbook/assets/Unifi_Symbol_400x400 (1).png" %}

## Sending Messages

* To send messages to specific users, operate bots, or integrate OA with external systems, you must use the **Messaging API**.
* [Messages API >](https://developers.line.biz/en/docs/messaging-api/)

## **(Optional) Multi-Language Welcome Message Automation**

<table><thead><tr><th>Step</th><th width="697">Details</th></tr></thead><tbody><tr><td>1</td><td>Create an OA channel on LINE Developers.</td></tr><tr><td>2</td><td><ul><li>Implement an API to receive Webhook events for the OA channel (used in Step 8).</li><li>method : POST</li><li><strong>URL</strong>: Flexible</li><li>Refer to the <a href="https://developers.line.biz/en/docs/messaging-api/receiving-messages/#webhook-event-in-one-on-one-talk-or-group-chat">Webhook specifications</a>.</li><li><a href="https://developers.line.biz/en/docs/messaging-api/receiving-messages/#verify-signature">It is recommended to verify the Webhook signature.</a></li></ul></td></tr><tr><td>3</td><td>When a <a href="https://developers.line.biz/en/reference/messaging-api/#follow-event">Follow Event </a>is received via the Webhook, retrieve the <code>userId</code> from the request body.</td></tr><tr><td>4</td><td><ul><li>Use the retrieved <code>userId</code> to fetch the user’s language setting on LINE.</li><li>Use the channel access token issued from the Messaging API tab in LINE Developers.</li><li>Utilize the <a href="https://developers.line.biz/en/reference/messaging-api/#get-profile">Get Profile API</a> to retrieve the user’s language.</li></ul></td></tr><tr><td>5</td><td><ul><li>Create templates for OA messaging. Configure the necessary content in multiple languages for each locale and store the templates locally or in the cloud. Refer to the <a href="https://developers.line.biz/en/reference/messaging-api/#message-objects">Message Objects API</a> for template formatting.</li><li><p>Example: For Korean and English support, save the templates as:</p><ul><li>oa_ko.json </li><li>oa_en.json</li></ul></li></ul></td></tr><tr><td>6</td><td>Load the appropriate template based on the user's language retrieved in Step 4, and call the <a href="https://developers.line.biz/en/reference/messaging-api/#send-push-message">OA Send API</a>.</td></tr><tr><td>7</td><td>Access the <strong>Messaging API</strong> tab in LINE Developers.<br><img src="../../.gitbook/assets/image-2025-1-9_15-47-22.png" alt=""></td></tr><tr><td>8</td><td><ul><li>Set the API endpoint developed in Steps 1–6 as the Webhook URL.</li><li>Turn the <strong>Use Webhook</strong> option to ON.</li></ul><p><img src="../../.gitbook/assets/image-2025-1-9_15-48-4.png" alt="" data-size="original"></p></td></tr><tr><td>9</td><td><p>After completing Step 8, followers will receive an automated welcome message in their  language.</p><p>(*Please make sure to turn OFF the welcome message setting in the existing Official Account Manager.)</p></td></tr></tbody></table>

## LINE OpenChat (Optional)

* Useful for two-way communication outside OA
* Available only in **Japan, Thailand, and Taiwan**
* You must have a LINE account registered in each country to create OpenChat there
* You may add **one translation bot**
  * Example: Korean ↔ English auto-translation

<figure><img src="../../.gitbook/assets/스크린샷 2024-12-12 오후 12.19.26.png" alt="" width="563"><figcaption></figcaption></figure>
