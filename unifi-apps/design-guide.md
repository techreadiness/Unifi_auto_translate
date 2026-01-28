# Design Guide

## Set Browser Tab Name

To indicate that it is a family service of the Unifi Apps ecosystem, please set the browser tab name in the format as `Name | Unifi Apps.`

<figure><img src="../.gitbook/assets/스크린샷 2025-02-04 오후 2.14.25.png" alt="" width="319"><figcaption></figcaption></figure>

## Set OpenGraph

The LINE MINI App and LINE Login LIFF/Web URLs of the Unifi Apps can be utilized across various marketing channels. If Open Graph is not set up, it may reduce the effectiveness of content delivery. Therefore, please ensure that Open Graph is properly configured. Without it, blank spaces or alternative text may appear where the link is displayed.

<figure><img src="../.gitbook/assets/OpenGraph.png" alt=""><figcaption></figcaption></figure>

## Connect Button

If Wallet Connect is integrated when initiating specific actions (such as Buy, NFT Airdrop, FT Airdrop, etc.) rather than using a standard button, please ensure that Wallet Connect is triggered when those actions are executed. It is acceptable for Wallet Connect not to be initiated based on the button guidelines provided. However, if you create a button similar to Wallet Connect, please make sure to adhere to the aforementioned guidelines.

<figure><img src="../.gitbook/assets/Unifi Connect Button Guide.png" alt=""><figcaption></figcaption></figure>

{% file src="../.gitbook/assets/Unifi_Symbol_400x400 (1).png" %}

{% file src="../.gitbook/assets/Unifi_Symbol_400x400 (1).svg" %}

## Set z-index for pop-up

z-index for SDK's pop-up to prevent blocking new windows from Browser set as '999'. Please set your z-index for any pup-up under '999' to avoid conflicting between pop-up's

