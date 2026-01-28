# Event Provider

<figure><img src="../.gitbook/assets/EventProvider_Unifi Apps Server.png" alt=""><figcaption></figcaption></figure>

## Event Provider Callback

### DappPortalSDK.getEventProvider()

Event Provider Callback for Unifi Apps Mission Completion

* The purpose of this callback method is to verify mission completion on Unifi side and automatically display a success banner when verification is successful.

```javascript
const eventProvider = DappPortalSDK.getEventProvider();

// When the mission is completed
const eventId: string = "eventId";          // Unique event ID provided by Unifi
const subMissionIndex: string = "1";        // Sub-mission index, starting from 0

await eventProvider.callback(eventId, subMissionIndex); // If verification is successful, a banner will be displayed automatically.
```

**Parameters**

<table><thead><tr><th width="164.28125">Parameter</th><th width="82.5703125">Type</th><th>Description</th></tr></thead><tbody><tr><td>eventId</td><td>string</td><td>The unique identifier provided by <strong>Unifi</strong></td></tr><tr><td>subMissionIndex</td><td>string</td><td>The index of the sub-mission provided by Unifi. Indexing starts from 0.<br>For example:<br>- Event item purchase Misson -> use subMissionIndex = "0"<br>- Lv4 achievement Misson -> use subMissionIndex = "1"</td></tr></tbody></table>

**Responses**

N/A

* If verification is successful, a banner will be displayed.

## Unifi Apps Server REST API Implementation

#### **Unifi Apps Server REST API Implementation Guide**&#x20;

To enable **mission completion** on the Unifi charts, the Unifi Apps server must provide an API endpoint that allows the Unifi to verify whether a mission has been completed.

* **Information Required**
  * API URL (required)
  * Custom Header (optional)
* **API Overview**
  * Metho&#x64;**:** <mark style="color:blue;">`GET`</mark>
  * Schem&#x65;**:** `https`
  * Read Timeou&#x74;**:** `1s`
    * If the Unifi server does not receive a response within **1 second**, the mission will be treated as **failed**.
* **Custom Header (optional)**
  * You may include a custom header when the API is called.
  * There are **no restrictions** on header key/value format.
  * **Only one** custom header can be used, and it is **optional**.
  * ex) x-dapp-custom-key: gq8g0Ah1MD98
* **URL Format**
  * Base UR&#x4C;**:** Unifi Apps server URL
  * The `$identifier` as query parameter must be included.
  * `$identifier` is a placeholder that will be replaced by the user’s wallet address (in lowercase) by the Unifi server.
  * ex) https://example.dapp.io/api/mission/1111?param=zzzz&**identifier=$identifier**
* **Response Body**
  * Content Typ&#x65;**:** JSON
  * If the Unifi server receives a successful response, the user is considered to have completed the mission.
    * Mission Complete
    * ```json
      HTTP/1.1 200 OK
      {
        "result": true
      }
      ```
    * Mission Fail
    * ```json
      HTTP/1.1 200 OK
      {
        "result": false
      }
      ```
